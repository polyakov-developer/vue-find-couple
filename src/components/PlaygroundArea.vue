<template>
  <div class="area d-flex" :style="{'height': 'auto', 'width': settings.width + 'px'}">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: {
    settings: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
.area {
  align-items: center;
  flex-wrap: wrap;
  justify-content: center;
  margin: auto;
  overflow: hidden;
}
</style>