<template>
  <div class="budgetListWrap">
    <el-card :header="header">
      <template v-if="!isEmpty">
        <div class="list-item" v-for="(item, prop) in list" :key="prop">
          <span class="budget-comment"> {{ item.comment }} </span>
          <span class="budget-value"> {{ item.value }} </span>
          <el-button type="danger" size="mini" @click="deleleteItem(item.id)">Delete</el-button>
        </div>
      </template>
      <el-alert v-else type="success" :title="emptyTitle" :closable="false"/>
    </el-card>
  </div>
</template>

<script>

export default {
  name: 'BudgetList',
  props: {
    list: {
      type: Object,
      defoult: () => ({})
    }
  },
  data: () => ({
    header: 'Budget List',
    emptyTitle: 'Your list is empty'
  }),
  computed: {
    isEmpty(){
      return !(Object.keys(this.list).length);
    }
  },
  methods: {
    deleleteItem(id) {
      this.$emit('deleteItem', id)
    }
  }
};
</script>

<style scoped>
.budgetListWrap {
  max-width: 500px;
  margin: auto;
}

.list-item {
  display: flex;
  align-items: center;
  padding: 10px 15px;
}

.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
</style>