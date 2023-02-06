<template>
  <div id="app">
    <FormBudget @submitForm="onFormSubmit" />
    <TotalBalance :total="totalBalance" />
    <BudgetList :list="list" @onDeleleteThisItem="onDeleteItem" />
  </div>
</template>

<script>
import BudgetList from "@/components/BudgetList";
import TotalBalance from "@/components/TotalBalance";
import FormBudget from "@/components/FormBudget";

export default {
  name: "App",
  components: {
    BudgetList,
    TotalBalance,
    FormBudget,
  },
  data: () => ({
    list: {
      1: {
        type: "INCOME",
        value: 180,
        comment: "1 some comment",
        id: 1,
      },
      2: {
        type: "OUTCOME",
        value: -50,
        comment: "2 some outcome comment",
        id: 2,
      },
      3: {
        type: "INCOME",
        value: 40,
        comment: "3 some comment",
        id: 3,
      },
      4: {
        type: "OUTCOME",
        value: -150,
        comment: "4 some outcome comment",
        id: 4,
      },
    },
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce((acc, item) => {
        acc +=
          item.type === "INCOME"
            ? (item.value = Math.abs(item.value))
            : (item.value = -Math.abs(item.value));
        return acc;
      }, 0);
    },
  },
  methods: {
    onDeleteItem(id) {
      this.$delete(this.list, id);
    },
    onFormSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random()),
      };

      this.$set(this.list, newObj.id, newObj);
    },
  },
  watch: {
    list() {
      return this.list;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
