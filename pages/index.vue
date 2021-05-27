<template>
  <div class="container">
    <div>
      <header-nav />
      <tag-nav :tag-list="tagList" />
    </div>
    <div class="main-container">
      <div class="main-container-left">
        <nav class="search-nav">
          <n-link class="search-nav-item" to="/" active-class="active"
            >热门</n-link
          >
          <n-link
            class="search-nav-item"
            to="/?sort=newest"
            active-class="active"
            >最新</n-link
          >
          <n-link
            class="search-nav-item"
            to="/?sort=three_days_hottest"
            active-class="active"
            >热榜</n-link
          >
        </nav>
        <div class="article-list">
          <div class="article-list-item" v-for="item of list">
            111
          </div>
        </div>
      </div>
      <div class="main-container-right"></div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  asyncData({ $axios }): Promise<object | void> | object | void {
    return $axios
      .$post(
        `https://api.juejin.cn/recommend_api/v1/article/recommend_all_feed`,
        {
          id_type: 2,
          client_type: 2608,
          sort_type: 200,
          cursor: '0',
          limit: 20,
        }
      )
      .then((res) => {
        const { err_no, data } = res
        return {
          list: err_no === 0 ? data : [],
        }
      })
  },
  data() {
    return {
      tagList: [
        {
          text: '推荐',
          path: '/recommended',
          active: true,
        },
        {
          text: '关注',
          path: 'following',
        },
        {
          text: '后端',
          path: 'backend',
        },
        {
          text: '前端',
          path: 'frontend',
        },
        {
          text: 'Android',
          path: 'android',
        },
        {
          text: 'iOS',
          path: 'ios',
        },
        {
          text: '人工智能',
          path: 'ai',
        },
        {
          text: '开发工具',
          path: 'freebie',
        },
        {
          text: '代码人生',
          path: 'career',
        },
        {
          text: '阅读',
          path: 'article',
        },
      ],
    }
  },
})
</script>

<style lang="scss" scoped>
.container {
  position: relative;
  margin: 0 auto;
  width: 100%;
  max-width: 960px;
  .main-container {
    margin-top: 10.833rem;
    display: flex;
    justify-content: space-around;
    .main-container-left {
      width: 700px;
      margin-right: 1.667rem;
      background-color: #ffffff;
      .search-nav {
        padding: 1.3rem 1rem;
        border-bottom: 1px solid hsla(0, 0%, 59.2%, 0.1);
        font-size: 14px;
        .search-nav-item {
          padding: 0 1.2rem;
          border-right: 1px solid hsla(0, 0%, 59.2%, 0.2);
          &.active {
            color: #007fff;
          }
          &:nth-last-child(1) {
            border-right: none;
          }
        }
      }
      .article-list {
        .article-list-item {
          cursor: pointer;
          padding: 16px 20px 0;
        }
      }
    }
    .main-container-right {
      flex: 1;
    }
  }
}
</style>
