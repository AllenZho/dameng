<template>
  <div class="background">
      <div class="box">
          <div class="panel clearfix">
              <div class="panel__left" :class="{'panel__left--full': !right}"><slot></slot></div>
              <div v-if="right" class="panel__right"><slot name="right"></slot></div>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    right: {
      type: Boolean,
      default: true
    }
  },
  data () {
    return {
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.background {
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background-image: url("~@/assets/background.jpg");
  background-size: cover;
}
.box {
  border-radius: 30px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 80%;
  /* height: 80%; */
  background: rgba(253, 235, 234, 0.6);
  padding: 10px;
  min-width: 960px;
  min-height: 650px;
  max-height: 90%;
}
.box::after {
  padding-bottom: 60%; /* 自适应比例 */
  content: "";
  position: static;
  display: inline-block;
  vertical-align: middle;
}
.panel {
  position: absolute;
  background: #fdfdfd;
  border-radius: 30px;
  width: calc(100% - 20px);
  height: calc(100% - 20px);
  left: 10px;
  top: 10px;
}
.panel__left {
  padding: 20px 40px;
  padding-right: calc(30% + 40px);
}
.panel__left--full {
  padding-right: 40px;
}
.panel__right{
  position: absolute;
  padding: 20px 30px;
  right: 0;
  top: 10px;
  height: calc(100% - 20px);
  width: 30%;
  box-shadow: -5px 0 30px -5px #eee;
  border-radius: 30px;
}
</style>
