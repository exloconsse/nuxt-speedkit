<template>
  <div v-font="$getFont('Merriweather', 300, 'italic')" class="layout-two-columns">
    <div><slot name="left" /></div>
    <div><slot name="right" /></div>
  </div>
</template>

<script>

export default {
  components: {

  }
};
</script>

<style lang="postcss">
.layout-two-columns {
  display: flex;

  & > div {
    width: calc(100% / 2);
    text-align: center;
  }
}
</style>
