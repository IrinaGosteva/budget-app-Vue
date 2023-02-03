<template>
  <div>
    <div class="list-item" v-for="(item, prop) in list" :key="prop">
      <span class="budget-comment"> {{ item.comment }} </span>
      <span class="budget-value"> {{ item.value }} </span>

      <el-button type="danger" size="mini" @click="centerDialogVisible = true"
        >Delete
      </el-button>
      <el-dialog
        title="Warning"
        :visible.sync="centerDialogVisible"
        width="30%"
        center
      >
        <span> {{ item.comment }} </span>
        <span slot="footer" class="dialog-footer">
          <el-button @click="centerDialogVisible = false">Cancel</el-button>
          <el-button
            type="primary"
            @click="(centerDialogVisible = false), deleteThisItem(item)"
            >Confirm</el-button
          >
        </span>
      </el-dialog>
    </div>
  </div>
</template>

<script>
export default {
  name: "BudgetListItem",
  data: () => ({
    centerDialogVisible: false,
  }),
  props: {
    list: {
      type: Object,
      defoult: () => ({}),
    },
  },
  methods: {
    deleteThisItem(item) {
      this.$emit("deleteThisItem", item.id);
    },
  },
};
</script>

<style scoped>
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
