<template>
  <default-layout>
    <v-header></v-header>
    <div class="title">
      <div class="title__left">Cards</div>
      <div class="title__right">View all Cards</div>
    </div>
    <div class="cards">
      <v-card
        v-for="item in cards"
        :key="item"
        class="card"
        :type="item % 2 === 0 ? 'primary' : 'danger'"
      />
      <div class="card card--add" @click="cards++">
        <div class="card__content">
          <div class="card__icon">
            <i class="el-icon-plus"></i>
          </div>
          <div class="card__tip">Add new Card</div>
        </div>
      </div>
    </div>
    <div class="main">
      <div class="service">
        <div class="title">
          <div class="title__left">Main Service</div>
          <div class="title__right">View all</div>
        </div>
        <div class="service-list">
          <div v-for="item in 6" :key="item" class="service-item">
            <div>
              <i class="el-icon-s-opportunity service-item__icon"></i>
              <div class="service-item__title">Transactions</div>
            </div>
          </div>
        </div>
      </div>
      <div class="statistics">
        <div class="current">
          <div class="title">
            <div class="title__left">Current</div>
            <div class="title__right">View all</div>
          </div>
          <div v-for="item in 3" :key="item" class="current-item">
            <div class="current-item__title">1063873637834</div>
            <div class="current-item__line"></div>
            <div class="current-item__price">$2,20001</div>
          </div>
        </div>
        <div class="saving">
          <div class="title">
            <div class="title__left">Savings</div>
            <div class="title__right">View all</div>
          </div>
          <div class="saving-box">
            <div ref="chart" class="chart"></div>
            <div class="count">
              <div class="count-item">
                <div class="count-item__title">Total</div>
                <div class="count-item_price">$100,09</div>
              </div>
              <div class="count-item">
                <div class="count-item__title">This week</div>
                <div class="count-item_price">$2567.89</div>
              </div>
              <div class="count-item">
                <div class="count-item__title">This month</div>
                <div class="count-item__price">$123.09</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div slot="right">
      <div class="side-header">
        <el-badge is-dot>
          <i class="el-icon-bell side-header__icon"></i>
        </el-badge>
        <div class="side-user">
          <div class="side-user__nickname">Anastasia</div>
          <img class="side-user__avatar" src="@/assets/logo.png" alt="">
        </div>
      </div>
      <div class="pie">
        <div>
          <div class="pie__price">$5,349</div>
          <div class="pie__title">Balance</div>
        </div>
      </div>
      <div class="side-title">
        <div>Transactions</div>
        <div>Today <i class="el-icon-arrow-down"></i></div>
      </div>
      <div class="side-item">
        <div class="side-item__icon">
          <i class="el-icon-s-data"></i>
        </div>
        <div class="side-item__title">Dribbble Pro Plan</div>
        <div class="side-item__price">-$100</div>
      </div>
      <div class="side-item">
        <div class="side-item__icon">
          <i class="el-icon-s-data"></i>
        </div>
        <div class="side-item__title">Adidas Refund</div>
        <div class="side-item__price side-item__price--success">+$230</div>
      </div>
      <div class="side-item">
        <div class="side-item__icon">
          <i class="el-icon-s-data"></i>
        </div>
        <div class="side-item__title">Wacom LCD</div>
        <div class="side-item__price">-$3000</div>
      </div>
      <div class="side-button">
        <div>Transfer Money</div>
        <i class="el-icon-right side-button__icon"></i>
      </div>
    </div>
  </default-layout>
</template>

<script>
import DefaultLayout from '@/components/layout/Default'
import VHeader from '@/components/common/Header'
import VCard from '@/components/common/Card'
import { debounce } from '@/assets/utils'
const echarts = require('echarts')
let chart = null
export default {
  components: { DefaultLayout, VHeader, VCard },
  name: 'HelloWorld',
  data () {
    return {
      cards: 2,
      chart: null
    }
  },
  mounted () {
    this.initChart()
    this.$_initResizeEvent()
  },
  beforeDestroy () {
    this.$_destroyResizeEvent()
  },
  methods: {
    initChart () {
      // 基于准备好的dom，初始化echarts实例
      chart = echarts.init(this.$refs.chart)
      // 绘制图表
      chart.setOption({
        grid: {
          top: 10,
          right: 20
        },
        xAxis: {
          type: 'category',
          data: ['$10', '$20', '$30', '$40', '$50']
        },
        yAxis: {
          type: 'value'
        },
        series: [{
          lineStyle: {
            width: 3,
            shadowColor: '#ccc',
            shadowBlur: 2,
            shadowOffsetY: 2,
            color: '#46c0db'
          },
          symbol: 'none',
          data: [10, 30, 26, 50, 58],
          type: 'line',
          smooth: true
        }]
      })
    },
    $_resizeHandler () {
      // 重绘图表
      return debounce(() => {
        if (chart) {
          chart.resize()
        }
      }, 100)()
    },
    $_initResizeEvent () {
      // 监听窗口尺寸大小变化
      window.addEventListener('resize', this.$_resizeHandler)
    },
    $_destroyResizeEvent () {
      // 注销监听
      window.removeEventListener('resize', this.$_resizeHandler)
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cards {
  display: flex;
  overflow-x: auto;
}
.card {
  width: 32%;
  margin-right: 2%;
  margin-bottom: 2%;
  flex-shrink:0
}
.card--add {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f8f8f8;
  border-radius: 10px;
  color: #d7d7d7;
  cursor: pointer;
}
.card--add::after {
  padding-bottom: 60%; /* 自适应比例 */
  content: "";
  position: static;
  display: inline-block;
  vertical-align: middle;
}
.card__content {
  text-align: center;
}
.card__icon {
  display: inline-block;
  padding: 4px;
  font-size: 26px;
  border: 1px dashed #d7d7d7;
  border-radius: 50%;
  margin-bottom: 10px;
}
.title {
  display: flex;
  justify-content: space-between;
  font-size: 16px;
  padding: 10px 0;
  margin-bottom: 10px;
}
.title__right {
  color: #999;
  font-size: 12px;
  cursor: pointer;
}
.service {
  width: 180px;
}
.service-list {
  display: flex;
  flex-wrap: wrap;
}
.service-item {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 80px;
  height: 80px;
  background-color: #fff;
  box-shadow: 5px 4px 5px 1px #eee;
  margin-bottom: 4%;
  border-radius: 5px;
  text-align: center;
  cursor: pointer;
}
.service-item:nth-child(2n) {
  margin-left: 20px;
}
.service-item__icon {
  font-size: 26px;
  color: #ff4d56;
  margin-bottom: 10px;
}
.service-item__title {
  font-size: 10px;
}
.main {
  display: flex;
  margin-top: 40px;
}
.statistics {
  /* flex: 1; */
  width: calc(100% - 200px);
  padding-left: 30px;
}
.current-item {
  display: flex;
  align-items: flex-end;
  padding: 8px 0;
  font-size: 12px;
}
.current-item__title {
  color: #999;
  padding-right: 10px;
}
.current-item__line {
  flex: 1;
  border-top: 1px dashed #ccc;
}
.current-item__price {
  padding-left: 10px;
}
.saving {
  margin-top: 10px;
}
.saving-box {
  display: flex;
  justify-content: space-between;
}
.chart {
  flex: 1;
  height: 170px;
  margin-top: 10px;
  /* width: calc(100% - 140px); */
}
.count {
  width: 120px;
  font-size: 12px;
}
.count-item {
  display: flex;
  justify-content: space-between;
  line-height: 1.8;
}
.count-item__title {
  color: #999;
  width: 100px;
}
.side-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.side-header__icon {
  font-size: 18px;
  color: #999;
  cursor: pointer;
}
.side-user {
  display: flex;
  align-items: center;
  font-size: 12px;
}
.side-user__avatar {
  width: 26px;
  height: 26px;
  border-radius: 50%;
  margin-left: 10px;
  cursor: pointer;
}
.pie {
  display: flex;
  align-items: center;
  justify-content: center;
  background-image: url(~@/assets/circle.png);
  background-size: 100% 100%;
  width: 170px;
  height: 170px;
  margin: 50px auto 40px;
  text-align: center;
}
.pie__price {
  font-size: 16px;
  font-weight: bold;
}
.pie__title {
  font-size: 12px;
  color: #999;
  margin-top: 4px;
}
.side-title {
  display: flex;
  justify-content: space-between;
  color: #999;
  margin-bottom: 20px;
}
.side-item {
  display: flex;
  align-items: center;
  font-size: 12px;
}
.side-item__icon {
  background-color: #fff;
  border-radius: 10px;
  color: #ff4d56;
  width: 50px;
  height: 50px;
  line-height: 50px;
  text-align: center;
  font-size: 24px;
}
.side-item__title {
  flex: 1;
}
.side-item__price {
  width: 70px;
  text-align: right;
  font-weight: bold;
  color: #ff4d56;
}
.side-item__price--success {
  color: #0e809a;
}
.side-button {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 90%;
  border-radius: 50px;
  margin: 40px auto 0;
  height: 50px;
  line-height: 50px;
  color: #fff;
  background-color: #ff4d56;
  padding: 0 20px;
  cursor: pointer;
}
.side-button__icon {
  font-size: 16px;
}
</style>
