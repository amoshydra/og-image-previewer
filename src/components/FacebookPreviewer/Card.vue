<template>
  <div
    class="fp"
    :class="cardType"
  >
    <div class="preview image">
      <img :src="data.src">
    </div>
    <div class="preview text">
      <div class="detail url"> {{ data.url }} </div>
      <div class="detail title"> {{ data.title }} </div>
      <div class="detail text"> {{ data.text }} </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    type: {
      type: String,
      default: 'mini',
    },
    data: {
      type: Object,
    },
  },
  computed: {
    cardType() {
      return `${this.type}-card`;
    },
  },
};
</script>

<style>
.fp {
  position: relative;
  background: white;
}

/* General */
.preview.text {
  font-family: Roboto, 'Droid Sans', Helvetica, sans-serif;
  color: #1c2028;
  line-height: 18px;
  font-size: 12px;
  display: flex;
  flex-flow: column;
}
.preview.text .detail {
  order: 1;
}
.preview.text .detail.url {
  text-transform: lowercase;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.preview.text .detail.title {
  font-weight: bold;
  overflow: hidden;
}

.preview.image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

/* Full card */
.fp.full-card {
  border: 1px solid #EBEBEB;
  max-width: 85%;

  border-top-right-radius: 1.3em;
  border-top-left-radius: 4px;
  border-bottom-right-radius: 1.3em;
  border-bottom-left-radius: 1.3em;
}
@media (min-width: 920px) {
  .fp.full-card {
    box-sizing: content-box;
    max-width: 70%;
  }
}
@media (min-width: 1211px) {
  .fp.full-card {
    max-width: 55%;
  }
}
@media (min-width: 1600px) {
  .fp.full-card {
      max-width: 60%;
  }
}
.fp.full-card .preview.image {
  min-height: 112px;
  padding-bottom: 52%;
  overflow: hidden;
  position: relative;
  box-sizing: border-box;
  border-top-right-radius: 1.3em;
  border-top-left-radius: 4px;
}
.fp.full-card .preview.image img {
  position: absolute;
  width: 100%;
}
.fp.full-card .preview.text {
  padding: 0 12px;
}
.fp.full-card .preview.text .detail.title {
  margin-top: 6px;
  line-height: 18px;
  height: 36px;
  -webkit-line-clamp: 2;
  font-size: 14px;
  font-family: "Helvetica Neue", "Segoe UI", Helvetica, Arial, sans-serif;
}
.fp.full-card .preview.text .detail.text {
  line-height: 16px;
  height: 32px;
  -webkit-line-clamp: 2;
  overflow: hidden;
}
.fp.full-card .preview.text .detail.url {
  order: 2;
  color: rgba(0, 0, 0, .40);
  margin-top: 6px;
  margin-bottom: 6px;
}


/* feed card */
.fp.feed-card {
  border: 1px solid #EBEBEB;
  max-width: 476px;
  width: 476px;
  box-shadow: 0 0 1px 0 rgba(0, 0, 0, .1) inset;
}
.fp.feed-card .preview.image {
  width: 476px;
  height: 249px;
  overflow: hidden;
  position: relative;
  box-sizing: border-box;
  border-bottom: 1px solid rgba(0, 0, 0, .1);
}

.fp.feed-card .preview.image img {
  width: 100%;
}
.fp.feed-card .preview.text {
  height: auto;
  margin: 10px 12px;
  /* max-height: 100px; */
}
.fp.feed-card .preview.text .detail.title {
  font-family: Georgia, serif;
  letter-spacing: normal;
  font-size: 18px;
  font-weight: 500;
  line-height: 22px;
  margin-bottom: 5px;
  max-height: 110px;
  word-wrap: break-word;
}
.fp.feed-card .preview.text .detail.text {
  line-height: 16px;
  max-height: 80px;
  overflow: hidden;
  -webkit-line-clamp: 5;
}
.fp.feed-card .preview.text .detail.url {
  padding-top: 9px;
  position: relative;
  text-transform: uppercase;
  order: 2;
  font-size: 11px;
  color: #90949c;
  font-family: Helvetica, Arial, sans-serif;
}


/* Mini card */
.fp.mini-card {
  max-width: 360px;
  height: 74px;
  border: 1px solid #EBEBEB;
  display: flex;
  background-color: #E8EAEE;
  overflow: hidden;
}
.fp.mini-card .preview.image {
  height: 74px;
  width: 74px;
  flex: 0 0 74px;
  background: white;
  overflow: hidden;
}
.fp.mini-card .preview.text {
  overflow: hidden;
  white-space: nowrap;
  margin: 12px;
  width: 100%;
}
.fp.mini-card .preview.text .detail.url {
  color: #464950;
}
.fp.mini-card .preview.text .detail.text {
  width: 100%;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* Mini chat card */
.fp.chat.mini-card {
  max-width: 164px;
  height: 72px;
  border-radius: 12px;
}
.fp.chat.mini-card .preview.image {
  height: 72px;
  width: 72px;
  flex: 0 0 72px;
}
.fp.chat.mini-card .preview.image img {
  border-top-left-radius: 12px;
  border-bottom-left-radius: 12px;
}
.fp.chat.mini-card .preview.text {
  margin-bottom: 4px;
  margin-left: 4px;
  margin-right: 6px;
  margin-top: 4px;
}
.fp.chat.mini-card .preview.text .detail.title {
  font-size: 12px;
  line-height: 16px;
  max-height: 32px;
  color: #1d2129;
  font-weight: bold;
  overflow: hidden;
  white-space: normal;
}
.fp.chat.mini-card .preview.text .detail.url {
  order: 2;
  font-size: 10px;
  line-height: 16px;
  color: #90949c;
  overflow: hidden;
  text-overflow: ellipsis;
}
.fp.chat.mini-card .preview.text .detail.text {
  font-size: 12px;
  line-height: 16px;
  color: #1d2129;
}


/* Mini app chat card */
.fp.app.chat.mini-card {
  max-width: 320px;
  height: 110px;
  border-radius: 12px;
  background: white;
}
.fp.app.chat.mini-card .preview.image {
  height: 110px;
  width: 110px;
  flex: 0 0 110px;
}
.fp.app.chat.mini-card .preview.text {
  margin: 12px;
}
.fp.app.chat.mini-card .preview.text .detail {
  line-height: 18px;
}
.fp.app.chat.mini-card .preview.text .detail.title {
  font-size: 16px;
  max-height: 36px;
  margin-bottom: 8px;
}
.fp.app.chat.mini-card .preview.text .detail.url {
  font-size: 14px;
}
.fp.app.chat.mini-card .preview.text .detail.text {
  font-size: 14px;
  margin-bottom: 8px;
}
</style>
