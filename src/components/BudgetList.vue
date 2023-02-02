<template>
  <div class="budgetListWrap">
    <el-card :header="header">
      <template v-if="!isEmpty">
        <BudgetListItem :list = 'list' @deleteThisItem ="onDeleleteThisItem"/>

      </template>
      <el-alert v-else type="success" :title="emptyTitle" :closable="false" />
    </el-card>
  </div>
</template>

<script>
import BudgetListItem from "./BudgetListItem";

export default {
  components: {
    BudgetListItem,
  },
  name: "BudgetList",
  props: {
    list: {
      type: Object,
      defoult: () => ({}),
    },
  },
  data: () => ({
    header: "Budget List",
    emptyTitle: "Your list is empty",
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    },
  },
  methods: {
    onDeleleteThisItem(id) {
      this.$emit("onDeleleteThisItem", id);
    },
  },
};
</script>

<style scoped>
.budgetListWrap {
  max-width: 500px;
  margin: auto;
}

</style>
