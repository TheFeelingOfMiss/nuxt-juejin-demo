<template>
  <div class="tag-nav-wrap">
    <div class="tag-nav-box">
      <n-link
        v-for="item of tagList"
        :key="item.path"
        :to="item.path"
        active-class="tag-link-active"
        class="tag-nav-item"
        :class="item.active ? 'tag-link-active' : ''"
        >{{ item.text }}</n-link
      >
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
export default Vue.extend({
  props: {
    tagList: {
      type: Array,
      default: () => [],
    },
  },
})
</script>

<style scoped lang="scss">
.tag-nav-wrap {
  width: 100%;
  height: 3.833rem;
  left: 0;
  top: 5rem;
  background-color: #ffffff;
  border-top: 1px solid #f1f1f1;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
  .tag-nav-box {
    width: 100%;
    height: 100%;
    max-width: 960px;
    margin: 0 auto;
    display: flex;
    align-items: center;
    .tag-nav-item {
      padding-right: 1rem;
      text-decoration: none;
      font-size: 1.16rem;
      color: #71777c;
      &.tag-link-active {
        color: #007fff;
      }
    }
  }
}
</style>
