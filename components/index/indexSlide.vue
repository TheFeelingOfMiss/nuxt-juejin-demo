<template>
  <ul ref="advertList" class="advert-list" :class="fixed ? 'fixed' : ''">
    <li v-for="item of list" :key="item.id" class="advert-list-item">
      <img :src="item.picture" />
    </li>
  </ul>
</template>

<script>
export default {
  name: 'IndexSlide',
  props: {
    list: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      // 固定定位
      fixed: false,
    }
  },
  mounted() {
    this.initScrollListener()
    this.scrollListener = window.addEventListener(
      'scroll',
      this.initScrollListener
    )
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.initScrollListener)
  },
  methods: {
    initScrollListener() {
      const scrollTop = document.scrollingElement.scrollTop
      // 滚动距离大于200隐藏导航
      if (
        scrollTop >
        this.$refs.advertList.offsetTop + this.$refs.advertList.offsetHeight
      ) {
        !this.fixed && (this.fixed = true)
        return
      }
      this.fixed && (this.fixed = false)
    },
  },
}
</script>

<style scoped lang="scss">
.advert-list {
  width: 240px;
  &.fixed {
    position: fixed;
  }
  .advert-list-item {
    img {
      width: 100%;
      object-fit: cover;
    }
  }
}
</style>
