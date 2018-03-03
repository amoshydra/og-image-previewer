<template>
  <div class="facebook-previewer">
    <h1>Facebook</h1>
    
    <h2>Facebook Post</h2>
    <CardWrapper>
      <Card type="feed" :data="cardInfo" />
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

export default {
  components: {
    CardWrapper,
    Card,
  },
  props: {
    src: {},
  },
  computed: {
    cardInfo() {
      return {
        src: this.src,
        url: this.url,
        title: this.title,
        text: this.text,
      };
    },
  },
  data() {
    return {
      url: 'strawberry.viddsee.com',
      title: 'Juree Philippines | Viddsee',
      text: 'Viddsee Juree Awards is a competition held to celebrate jury’s picks of Asian short films from all genres: fiction, documentary and animation.',
    };
  },
};
</script>

<style>
.facebook-previewer {

}
</style>
