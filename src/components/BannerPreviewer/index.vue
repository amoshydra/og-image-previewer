<template>
  <div>
    <h1>Banner</h1>

    <h2>Aspect ratio 3 : 1</h2>
    <div class="banner-container mobile">
      <div class="aspect r-16-9" :style="backgroundStyle"></div>
    </div>

    <h2>Aspect ratio 16 : 9</h2>
    <div class="banner-container desktop">
      <div class="aspect r-3-1" :style="backgroundStyle"></div>
    </div>

  </div>
</template>

<script>
export default {
  props: {
    src: {},
  },
  computed: {
    backgroundStyle() {
      if (!this.src) return {};
      return {
        backgroundImage: `url("${this.src}")`,
      };
    },
  },
};
</script>

<style>
.banner-container {
  box-shadow: 1px 1px 1px 1px rgba(0,0,0,0.1);
  position: relative;
  max-width: 100%;
}
.banner-container.desktop {
  width: 100%;
}
.banner-container.mobile {
  width: 480px;
}

.aspect {
  width: 100%;
  background-size: cover;
  background-position: center;
}
.aspect.r-16-9 {
  padding-top: 56.25%
}
.aspect.r-3-1 {
  padding-top: 33.33%
}

</style>
