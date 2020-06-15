<template lang="pug">
.pages-index
  p.pages-index__title aaaa
  .parent#parent(:style="{height:parentHeight}")
  .child#child
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  data() {
    return {
      parentHeight: '0px',
    }
  },
  methods: {
    handleResize() {
      // childを取得し、親要素に高さを付与する。
      const child = document.getElementById('child')
      if (child != null) {
        let childHeight: number = child.clientHeight;
        this.parentHeight = `${100 + childHeight}px`;
      }
    }
  },
  mounted() {
    // 読み込み時にイベント発火。
    window.addEventListener('DOMContentLoaded', this.handleResize)
    // windowサイズが変化するたびにイベント発火。
    window.addEventListener('resize', this.handleResize)
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.handleResize)
  }
});
</script>

<style lang="scss">
.pages-index {
  &__title {
    color: red;
  }

  .parent {
    width: 100px;
    height: 100px;
    background: blue;
  }

  .child {
    width: 100px;
    height: 100px;
    background: green;
  }
}

</style>
