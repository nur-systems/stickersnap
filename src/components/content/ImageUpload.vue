<template>
  <b-field>
    <b-upload v-model="files" multiple drag-drop expanded @input="emitFiles()" accept="image/*">
      <section class="section">
        <div class="content has-text-centered">
        <p>
          <b-icon icon="robot" size="is-large"></b-icon>
        </p>
        <p>
          Drop your picture here or tap to upload!
        </p>
      </div>
    </section>
    </b-upload>
  </b-field>
</template>

<script>
  export default {
    data: function () {
      return {
        files: []
      }
    }, 
    methods: {
      emitFiles: function () {
        const uniqueFiles = this.files.filter((v, i, a) => a.indexOf(v) === i); 
        this.$emit('upload', uniqueFiles);
      }
    }
  }
</script>