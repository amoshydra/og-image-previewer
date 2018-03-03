<template>
  <div id="app">

    <vue-dropzone
      id="dropzone"
      class="dropzone"
      ref="myVueDropzone"
      :options="dropzoneOptions"
      @vdropzone-thumbnail="updatePreview"
    />

    <div class="previewer">
      <BannerPreviewer
        :src="previewUrl"
      />
    </div>

    <div class="previewer">
      <FacebookPreviewer
        :src="previewUrl"
      />
    </div>
  </div>
</template>

<script>
import vue2Dropzone from 'vue2-dropzone';
import 'vue2-dropzone/dist/vue2Dropzone.css';
import FacebookPreviewer from './components/FacebookPreviewer';
import BannerPreviewer from './components/BannerPreviewer';

export default {
  name: 'App',
  components: {
    FacebookPreviewer,
    BannerPreviewer,
    vueDropzone: vue2Dropzone,
  },
  data() {
    return {
      dropzoneOptions: {
        url: ' ',
        dictDefaultMessage: 'Drop image to preview',
        autoProcessQueue: false,
      },
      previewUrl: false,
    };
  },
  methods: {
    getBase64(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = function () {
          resolve(reader.result);
        };
        reader.onerror = function (error) {
          reject(error);
        };
      })
    },
    updatePreview(file) {
      this.getBase64(file)
        .then((dataUrl) => {
          this.previewUrl = dataUrl;
        })
    },
  },
};
</script>

<style>
body {
  padding: 0;
  margin: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #F3f3f3;
  padding: 24px;
}

.previewer {
  margin-top: 24px;
  margin-bottom: 64px;
  padding: 24px 64px;
  padding-bottom: 48px;
  max-width: 1200px;
  margin-left: auto;
  margin-right: auto;
  background-color: #FFF;
}

.dropzone {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(255, 255, 255, 0.95);
  z-index: 1;
}

.dropzone.dz-started {
  background: rgba(255, 255, 255, 0.0);
  z-index: 0;
}

.dropzone.vue-dropzone:hover {
  background: rgba(255, 255, 255, 0.9);
}
.dropzone.dz-started.vue-dropzone:hover {
  background: rgba(255, 255, 255, 0.0);
}

.dropzone.dz-drag-hover {
  z-index: 1;
  background: rgba(200, 255, 220, 0.5);
}

.dropzone .dz-preview {
  display: none;
}
</style>
