<template>
  <div class="container">
    <div>
      <header-nav>
        <tag-nav :tag-list="tagList" slot="tag" />
      </header-nav>
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
        <div v-if="list.length > 0" class="article-list">
          <div
            v-for="item of list"
            :key="item.item_info.article_id"
            class="article-list-item"
          >
            <template>
              <div class="article-header">
                <div class="user-info">
                  <span class="user-name">{{
                    item.item_info.author_name ||
                    item.item_info.author_user_info.user_name
                  }}</span>
                  <span class="time">1小时前</span>
                </div>
                <div v-if="item.item_type === 14" class="tag-list">
                  <el-tag
                    v-for="tagItem of item.item_info.tags"
                    :key="tagItem.id"
                    class="tag"
                    type="info"
                    size="mini"
                    >{{ tagItem.tag_name }}</el-tag
                  >
                </div>
              </div>
              <div class="article-title">
                {{ item.item_info.title || item.item_info.article_info.title }}
              </div>
              <div class="article-content-wrap">
                <div class="article-content-box">
                  <div class="article-content">
                    {{
                      item.item_info.brief ||
                      item.item_info.article_info.brief_content
                    }}
                  </div>
                  <div v-if="item.item_type === 2" class="article-action">
                    <div class="article-action-item">
                      <i class="el-icon-thumb" />
                      <span>{{ item.item_info.article_info.digg_count }}</span>
                    </div>
                    <div class="article-action-item">
                      <i class="el-icon-chat-round" />
                      <span>{{
                        item.item_info.article_info.comment_count
                      }}</span>
                    </div>
                    <div class="article-action-item">
                      <i class="el-icon-share"></i>
                      <span>分享</span>
                    </div>
                  </div>
                </div>
                <div
                  v-if="
                    item.item_info.picture ||
                    item.item_info.article_info.cover_image
                  "
                  class="article-picture"
                >
                  <img
                    :src="
                      item.item_info.picture ||
                      item.item_info.article_info.cover_image
                    "
                  />
                </div>
              </div>
            </template>
          </div>
        </div>
      </div>
      <div class="main-container-right">
        <index-slide :list="adverts" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  async asyncData({ $axios }) {
    // 获取广告
    const getAdverts = $axios.$post(
      `https://api.juejin.cn/content_api/v1/advert/query_adverts`,
      {
        layout: 1,
        platform: 2608,
        position: 100,
      }
    )
    // 获取文章列表
    const getArticles = $axios.$post(
      `https://api.juejin.cn/recommend_api/v1/article/recommend_all_feed`,
      {
        id_type: 2,
        client_type: 2608,
        sort_type: 200,
        cursor: '0',
        limit: 20,
      }
    )
    const [advertsRes, articlesRes] = await Promise.all([getAdverts, getArticles])
    return {
      adverts: advertsRes.err_no === 0 ? advertsRes.data : [],
      list: articlesRes.err_no === 0 ? articlesRes.data : [],
    }
  },
  scrollToTop: true,
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
          .article-header {
            height: 22px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 14px;
            .user-info {
              overflow: hidden;
              .user-name {
                border-right: 1px solid #e5e6eb;
                padding-right: 8px;
                margin-right: 8px;
              }
            }
            .tag-list {
              .tag {
                margin-left: 8px;
              }
            }
          }
          .article-title {
            margin-top: 14px;
            margin-bottom: 12px;
            font-weight: 700;
            font-size: 18px;
            line-height: 24px;
            color: #1d2129;
            word-break: break-all;
          }
          .article-content-wrap {
            width: 100%;
            padding-bottom: 16px;
            display: flex;
            justify-content: space-between;
            border-bottom: 1px solid #e5e6eb;
            .article-content-box {
              .article-content {
                height: 44px;
                margin-bottom: 14px;
                font-size: 14px;
                line-height: 22px;
                overflow: hidden;
                text-overflow: ellipsis;
                display: -webkit-box;
                -webkit-line-clamp: 2;
                -webkit-box-orient: vertical;
                color: #4e5969;
              }
              .article-action {
                display: flex;
                .article-action-item {
                  margin-right: 32px;
                  font-size: 14px;
                  line-height: 20px;
                  color: #86909c;
                  span {
                    margin-left: 4px;
                  }
                }
              }
            }
            .article-picture {
              flex: 0 0 auto;
              width: 142px;
              height: 80px;
              margin-left: 16px;
              background-color: #fff;
              border-radius: 2px;
              img {
                width: 100%;
                height: 100%;
                object-fit: cover;
              }
            }
          }
        }
      }
    }
    .main-container-right {
      flex: 1;
    }
  }
}
</style>
