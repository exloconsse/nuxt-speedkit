<template>
  <div class="scroll-container" :class="{'direction-horizontal': directionHorizontal}">
    <scroll-item
      v-for="(item, index) in items"
      :key="index"
      :class="`item item-${index}`"
      :index="index"
      v-bind="item"
    />
  </div>
</template>
<script>
import ScrollItem from '../atoms/ScrollItem';
export default {
  components: {
    ScrollItem
  },
  props: {
    directionHorizontal: {
      type: Boolean,
      default: false
    },
    items: {
      type: Array,
      required: true
    }
  }
};
</script>
<style lang="postcss" scoped>
.scroll-container {
  width: 100%;
  height: 100%;
  overflow-x: hidden;
  overflow-y: scroll;

  & .item + .item {
    margin-top: em(20px);
  }

  &.direction-horizontal {
    display: flex;
    overflow-x: scroll;
    overflow-y: hidden;

    & .item {
      flex: 0 0 50vw;
    }

    & .item + .item {
      margin-top: 0;
      margin-left: em(20px);
    }
  }
}
</style>
