<template>
  <div id="app">

    <vue-dropzone
      id="dropzone"
      class="dropzone"
      :class="!!previewUrl ? 'has-picture' : ''"
      ref="myVueDropzone"
      :options="dropzoneOptions"
      @vdropzone-thumbnail="updatePreview"
    />

    <div class="previewer" style="position: relative; z-index: 100;">
      <input
        v-model="requestedUrl"
        style="
          box-sizing: border-box;
          width: calc(100% - 100px);
          padding: 10px 8px;
          border: 1px solid rgba(0,0,0,0.1);
        "
        placeholder="picture url"
      >
      <button
        @click="requestUrl"
        style="
          box-sizing: border-box;
          width: 90px;
          padding: 10px 8px;
          border: none;
        ">Use image</button>
    </div>
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
    const searchString = location.search.match(/\?i=(.*)/);
    const queryUrl = searchString ? searchString[1] : null;
    return {
      dropzoneOptions: {
        url: ' ',
        dictDefaultMessage: 'Drop image to previeyw',
        autoProcessQueue: false,
      },
      requestedUrl: queryUrl || 'https://images.pexels.com/photos/255419/pexels-photo-255419.jpeg?w=3840&h=1280&auto=compress&cs=tinysrgb',
      previewUrl: queryUrl || false,
    };
  },
  methods: {
    getBase64(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.readAsDataURL(file);
        reader.onload = () => {
          resolve(reader.result);
        };
        reader.onerror = (error) => {
          reject(error);
        };
      });
    },
    updatePreview(file) {
      this.getBase64(file)
        .then((dataUrl) => {
          this.previewUrl = dataUrl;
        });
    },
    requestUrl() {
      if (this.requestedUrl && this.requestedUrl.trim()) {
        this.previewUrl = this.requestedUrl;
      }
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
  padding-top: 24px;
}

.previewer {
  margin-top: 24px;
  margin-bottom: 64px;
  margin-left: 24px;
  margin-right: 24px;
  padding: 24px 8px;
  padding-bottom: 48px;
  max-width: 1200px;
  margin-left: auto;
  margin-right: auto;
  background-color: #FFF;
}

@media (min-width: 480px) {
  .previewer {
    padding-left: 24px;
    padding-right: 24px;
  }
}

@media (min-width: 768px) {
  .previewer {
    padding-left: 64px;
    padding-right: 64px;
  }
}

.dropzone {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(255, 255, 255, 1);
  z-index: 1;
  cursor: pointer;
}

.dropzone .dz-default.dz-message {
  font-size: 32px;
}
.dropzone.has-picture .dz-default.dz-message {
  display: none;
}

.dropzone.has-picture,
.dropzone.dz-started {
  background: rgba(255, 255, 255, 0.0);
  z-index: 0;
}

.dropzone.vue-dropzone:hover {
  background: rgba(255, 255, 255, 0.99);
}
.dropzone.has-picture.vue-dropzone:hover,
.dropzone.dz-started.vue-dropzone:hover {
  background: rgba(255, 255, 255, 0.0);
}

.dropzone.dz-drag-hover {
  z-index: 1;
  background: rgba(200, 255, 220, 0.5);
}

.dropzone .dz-preview {
  display: none !important;
}
</style>
