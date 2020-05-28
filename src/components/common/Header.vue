<template>
  <div class="header clearfix">
    <img src="@/assets/logo.png" alt class="header-logo" />
    <ul class="header-nav">
      <li class="header-nav__item header-nav__item--active">Dashboard</li>
      <li class="header-nav__item">Service</li>
      <li class="header-nav__item">History</li>
      <li class="header-nav__item">Actions</li>
    </ul>
    <div class="header-search">
      <el-input
        class="header-search__input"
        suffix-icon="el-icon-search"
        placeholder="search..."
        size="small"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}
.header-logo {
  width: 40px;
  height: 40px;
  margin-top: -10px;
  cursor: pointer;
}
.header-content {
  width: calc(100% - 50px);
  float: right;
}
.header-nav {
  flex: 1;
  font-size: 0;
  height: 50px;
  max-width: calc(100% - 190px);
  text-align: center;
}
.header-nav::after {
  content: "";
  display: inline-block;
  vertical-align: middle;
  height: 100%;
  line-height: 100%;
}
.header-nav__item {
  display: inline-block;
  vertical-align: middle;
  font-size: 14px;
  color: #666;
  padding: 10px;
}
.header-nav__item:hover {
  color: #333;
  cursor: pointer;
}
.header-nav__item.header-nav__item--active {
  color: #333;
  font-size: 16px;
}
.header-search {
  width: 180px;
  background-color: #eee;
  border-radius: 50px;
  overflow: hidden;
  border: none;
}
.header-search /deep/ input {
  background-color: #eee !important;
  border: none;
}
</style>
