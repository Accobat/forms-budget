<template>
  <div class="total-value">
    <h1 class="big" v-if="total > 0">Balance: {{ total }}</h1>
    <h1 class="small" v-if="total < 0">Balance: {{ total }}</h1>
    <h1 class="equals" v-if="total == 0">Balance: {{ total }}</h1>
  </div>

</template>

<script>
export default {
  name: "TotalBalance",
  props: {
    total: {
      type: Number,
      default: 0
    }
  }
};
</script>

<style scoped>
.total-value .big {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
  color: #0da50df1;
}
.total-value .small {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
  color: #cc3535;
}
.total-value .equals {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
  color: black;
}
</style>