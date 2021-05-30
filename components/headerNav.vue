<template>
  <div class="header-box-wrap" :class="headerShow ? 'show' : 'hide'">
    <div class="header-box">
      <header class="header-nav">
        <div class="nav-list">
          <n-link to="/" class="logo">
            <img src="~assets/image/logo.svg" />
          </n-link>
          <n-link to="/" active-class="nav-link-active" class="nav-link">
            首页
          </n-link>
          <n-link to="/pins" class="nav-link" active-class="nav-link-active">
            沸点
          </n-link>
          <n-link to="/books" class="nav-link" active-class="nav-link-active">
            小册
          </n-link>
          <n-link
            to="/event/all"
            class="nav-link"
            active-class="nav-link-active"
          >
            活动
          </n-link>
        </div>
        <el-input
          class="search-input"
          size="small"
          placeholder="探索掘金"
          suffix-icon="el-icon-search"
        />
        <el-button size="small" type="primary"> 创作者中心 </el-button>
        <el-button size="small" type="primary"> 写文章 </el-button>
        <el-button size="small" type="primary" plain> 登录 </el-button>
      </header>
    </div>
    <slot name="tag" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      // 头部导航显示
      headerShow: true,
      // 滚动监听
      scrollListener: null,
    }
  },
  mounted() {
    this.initScrollListener()
    this.scrollListener = window.addEventListener(
      'scroll',
      this.initScrollListener
    )
  },
  methods: {
    initScrollListener() {
      const scrollTop = document.scrollingElement.scrollTop
      // 滚动距离大于200隐藏导航
      if (scrollTop > 200) {
        this.headerShow && (this.headerShow = false)
        return
      }
      !this.headerShow && (this.headerShow = true)
    },
  },
  beforeDestroy() {
    window.removeEventListener('scroll', this.initScrollListener)
  },
}
</script>

<style lang="scss">
.header-box-wrap {
  position: fixed;
  width: 100%;
  left: 0;
  top: 0;
  background-color: #ffffff;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
  transition: all 0.2s;
  z-index: 2;
  &.show {
    transform: translateY(0);
  }
  &.hide {
    transform: translateY(-5rem);
  }
  .header-box {
    .header-nav {
      margin: 0 auto;
      width: 100%;
      height: 5rem;
      max-width: 960px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      .nav-list {
        flex: 1;
        display: flex;
        align-items: center;
        .logo {
          margin-right: 2rem;
        }
        .nav-link {
          color: #71777c;
          font-size: 16px;
          text-decoration: none;
          padding: 0 1.5rem;
          &.nav-link-active {
            color: #007fff;
          }
        }
      }
      .search-input {
        width: 168px;
        margin-right: 10px;
      }
    }
  }
}
</style>
