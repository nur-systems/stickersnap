<template>
  <div class="card">
    <div class="card-image has-text-centered">
      <section>
        <b-notification :active.sync="errorActive" type="is-danger" has-iconaria-close-label="Close notification">
          <p class="title is-6 has-text-weight-bold ">Error!</p>
          <p class="subtitle is-7">The image could not be processed!</p>
          <p class="subtitle is-7">This can happen because you uploaded an invalid file type or the system is overloaded. Try again, and if the problem persists, contact <a href="https://nur.wtf">Nur</a>.</p>
        </b-notification>
      </section>
      <img :src="imageURL()" class="image" style="object-fit: contain; height: 256px; max-width: 100%;">
      <b-progress v-if="!isProcessed" type="is-success" size="is-small"></b-progress>
    </div> 
     
    <div class="card-content">
      <p class="title is-4 has-text-centered">{{ name() }}</p>
    </div>

    <footer class="card-footer">
      <a class="card-footer-item" :disabled="!isProcessed" :download="name() + '.png'" :href="imageURL()">
        <b-icon icon="download"></b-icon>
        <span>Download</span>
      </a>

      <a class="card-footer-item" v-on:click="$emit('delete')">
        <b-icon icon="trash"></b-icon>
        <span>Delete</span>
      </a>
    </footer>
  </div>
</template>


<script>
import axios from 'axios'

  export default {
    props: ['file', 'modelSvcUrl'],
    data() {
      return {
        stickerURL: null,
        isProcessed: false,
        errorActive: false
      }
    },
    methods: {
      removeFormat: function (value) {
        return value.split('.').slice(0, -1).join('.');
      },
      name: function () {
        return this.removeFormat(this.file.name);
      },
      imageURL: function () {
        if (this.stickerURL == null) {
          return URL.createObjectURL(this.file);
        } else {
          return this.stickerURL;
        }
      },
      fetchSticker: function (file) {
        let URL = this.modelSvcUrl;
        let data = new FormData();
        let config = {
          responseType: 'arraybuffer',
          crossDomain: true
        }
        data.append('data', file); 
        axios.post(URL, data, config).then(
          response => {
            let bytes = new Uint8Array(response.data);
            let binary = bytes.reduce((data, b) => data += String.fromCharCode(b), '');
            let base64 = btoa(binary);

            this.isProcessed = true;
            this.stickerURL = 'data:image/png;base64,' + base64
          }
        ).catch(error => {
          this.errorActive = true;
          this.isProcessed = true;
          console.log(error);
        })
      }
    }, 
    beforeMount: function () {
      this.fetchSticker(this.file);
    }
  }
</script>