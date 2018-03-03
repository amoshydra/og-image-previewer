<template>
  <div class="facebook-previewer">
    <h1>Facebook</h1>

    <div>
      <input
        type="text"
        class="fp-input"
        v-model="title"
        placeholder="title"
      >
      <textarea
        class="fp-input"
        v-model="text"
        placeholder="text"
      ></textarea>
      <input
        type="text"
        class="fp-input"
        v-model="url"
        placeholder="url"
      >
    </div>

    <h2>Facebook Post</h2>
    <CardWrapper>
      <Card type="feed" :data="cardInfo" />
      <Card type="android feed" :data="cardInfo" />
    </CardWrapper>

    <h2>Facebook Chat</h2>
    <CardWrapper>
      <Card type="mini" :data="cardInfo" />
      <Card type="chat mini" :data="cardInfo" />
      <Card type="app chat mini" :data="cardInfo" />
      <Card type="full" :data="cardInfo" />
    </CardWrapper>
  </div>
</template>

<script>
import Card from './Card';
import CardWrapper from './CardWrapper';

const defaultText = {
  url: 'http://example.com/',
  title: 'Example Domain',
  text: 'This domain is established to be used for illustrative examples in documents. You may use this domain in examples without prior coordination or asking for permission.',
};

export default {
  components: {
    CardWrapper,
    Card,
  },
  props: {
    src: {},
  },
  data() {
    const cachedInfoString = localStorage.getItem('card-info');
    let parsed = {};
    try {
      parsed = JSON.parse(cachedInfoString) || {};
    } catch (error) {
      parsed = {};
    }

    return {
      url: parsed.url || defaultText.url,
      title: parsed.title || defaultText.title,
      text: parsed.text || defaultText.text,
    };
  },
  computed: {
    cardInfo() {
      return {
        src: this.src,
        url: this.url.trim() || defaultText.url,
        title: this.title.trim() || defaultText.title,
        text: this.text.trim() || defaultText.text,
      };
    },
  },
  watch: {
    cardInfo(info) {
      localStorage.setItem('card-info', JSON.stringify({
        url: info.url,
        title: info.title,
        text: info.text,
      }));
    },
  },
};
</script>

<style>
.fp-input {
  font-family: Arial, Helvetica, sans-serif;
  display: block;
  margin-bottom: 12px;
  padding: 8px;
  padding-bottom: 12px;
  max-width: 600px;
  width: 100%;
  position: relative;
  border: 1px solid rgba(0,0,0,0.1);
  box-shadow: 1px 1px 1px 1px rgba(0,0,0,0.05);
}

textarea.fp-input {

}
</style>
