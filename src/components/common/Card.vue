<template>
  <div class="card" :class="`card--${type}`">
    <div class="card__content">
      <div>
        <div class="card__circle"></div>
        <div class="card__circle card__circle--second"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'card',
  props: {
    type: {
      type: String,
      default: 'danger'
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
.card {
  border-radius: 10px;
  background-color: #0e809a;
  position: relative;
  display: block;
  overflow: hidden;
  color: #084a57;
}
.card--primary {
  background-color: #0e809a;
}
.card--danger {
  background-color: #ff4d56;
}
.card--warning {
  background-color: #e9b158;
}
.card::after {
  padding-bottom: 60%; /* 自适应比例 */
  content: "";
  position: static;
  display: inline-block;
  vertical-align: middle;
}
.card__content {
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  max-height: 100%;
  padding: 10px;
  display: flex;
  align-items: flex-end;
  justify-content: flex-end;
}
.card__circle {
  border-radius: 50%;
  width: 20px;
  height: 20px;
  background-color: #e30613;
  display: inline-block;
}
.card__circle--second {
  background-color: #ffc24b;
  margin-left: -12px;
}
.card--primary.card__circle {
  background-color: #ff3a4f;
}
</style>
