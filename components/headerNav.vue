<template>
  <div class="header-box-wrap">
    <div class="header-box">
      <header class="header-nav">
        <n-link to="/" class="logo">
          <img src="~assets/image/logo.svg" />
        </n-link>
        <n-link to="/" active-class="nav-link-active" class="nav-link">
          首页
        </n-link>
        <n-link to="/pins" class="nav-link"> 沸点 </n-link>
        <n-link to="/books" class="nav-link"> 小册 </n-link>
        <n-link to="/event/all" class="nav-link"> 活动 </n-link>
        <el-input size="small"
          placeholder="探索掘金"
        />
        <el-button>
          创作者中心
        </el-button>
        <el-button>
          写文章
        </el-button>
        <el-button>
          登录
        </el-button>
      </header>
    </div>
  </div>
</template>

<style lang="scss">
.header-box-wrap {
  position: fixed;
  width: 100%;
  left: 0;
  top: 0;
  .header-box {
    margin: 0 auto;
    width: 100%;
    max-width: 960px;
    .header-nav {
      height: 5rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      .nav-link {
        color: #71777c;
        font-size: 16px;
        text-decoration: none;
        &.nav-link-active {
          color: #007fff;
        }
      }
    }
  }
}
</style>
