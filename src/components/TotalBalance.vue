<template>
  <div class="total-value" @change="changeTotalColor" :style="{ color: color }">
    Balance {{ total }}
  </div>
</template>

<script>
export default {
  name: "TotalBalance",
  data: () => ({
    color: "",
  }),
  props: {
    total: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    changeTotalColor() {
      let x = this.total;
      if (x > 0) {
        this.color = "green";
      } else if (x !== 0) {
        this.color = "red";
      } else {
        this.color = "#2c3e50";
      }
    },
  },
  mounted() {
    this.changeTotalColor();
  },
  watch: {
    total() {
      this.changeTotalColor();
    },
  },
};
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}
</style>
