<template>
  <div class="sortItem">
    <el-button
      class="el-button el-button--success is-plain el-icon-top"
      @click="sortList('INCOME')"
    >
    </el-button>
    <el-button
      class="el-button el-button--danger is-plain el-icon-bottom"
      @click="sortList('OUTCOME')"
    >
    </el-button>
    <el-button class="el-button el-button--plain is-plain" @click="sortList()"
      >All
    </el-button>
  </div>
</template>

<script>
export default {
  name: "SortElements",
  data: () => ({
    sortedList: [],
  }),
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  methods: {
    sortList(value) {
      this.$emit("sortList", value);
    },
  },
};
</script>

<style scoped>
.sortItem {
  text-align: right;
  padding: 10px 15px;
}
</style>
