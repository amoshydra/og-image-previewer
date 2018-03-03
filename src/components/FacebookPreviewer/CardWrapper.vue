<template>
  <div class="card-wrapper">
    <slot></slot>
  </div>
</template>

<script>
export default {
}
</script>

<style>
.card-wrapper .fp {
  margin-bottom: 40px;
}
.card-wrapper .fp:first-of-type {
  margin-top: 40px;
}
</style>
