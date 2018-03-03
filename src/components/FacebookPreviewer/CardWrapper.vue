<template functional>
  <div class="card-wrapper">
    <slot />
  </div>
</template>

<script>
export default {
  render(createElement, context) {
    return createElement(
      context.children,
    );
  },
};
</script>

<style>
.card-wrapper .fp {
  margin-bottom: 40px;
}
.card-wrapper .fp:first-of-type {
  margin-top: 40px;
}
</style>
