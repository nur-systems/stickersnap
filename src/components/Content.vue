<template>
  <section class="content">
    <div class="container">
      <div class="columns is-centered">
        <div class="column is-8 level">
          <hr>
          
          <p class="subtitle">Create the best stickers for Whatsapp or Telegram from your camera roll using Artificial Intelligence!</p>

          <div class="container">
            <b-tabs :animated="false" v-model="activeTab">
              <b-tab-item label="Upload">
                <ImageUpload v-bind:files="files" @upload="processFiles"></ImageUpload>
              </b-tab-item>

              <b-tab-item label="Stickers">
                <div class="columns">
                  <div class="column is-12">
                    <b-button type="is-large is-danger" :disabled="files.length == 0" icon-left="robot" expanded @click="files = [];">
                      {{ files.length > 0 ? 'I want to start over!' : 'Waiting for images!' }}
                    </b-button>
                  </div>
                </div>
                <div class="columns is-multiline">
                  <div v-for="(file, index) in files" :key="index" class="column is-4">
                    <Sticker v-bind:file="file" 
                             v-bind:modelSvcUrl="modelSvcUrl"
                             @delete="deleteFile(index)"></Sticker>
                  </div>
                </div>
              </b-tab-item>

              <b-tab-item label="Dev. Tools">
                <DevTools v-bind:modelSvcUrl="modelSvcUrl"></DevTools>
              </b-tab-item>
            </b-tabs>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>


<script>
import ImageUpload from './content/ImageUpload.vue'
import Sticker from './content/Sticker.vue'
import DevTools from './content/DevTools.vue'

  export default {
    components: {
      Sticker,
      DevTools,
      ImageUpload
    },
    data: function () {
      return {
        files: [],
        activeTab: 0,
        modelSvcUrl: process.env.VUE_APP_PHOTO_STICKER_SVC,
      }
    },
    methods: {
      deleteFile: function (index) {
        this.files.splice(index, 1);
        this.files = this.files.map(x => x);
      },
      processFiles: function (files) {
        this.files = files;
        this.activeTab = 1;
      }
    }
  }
</script>