<template>
  <div>
    <SortElements @sortList="sortElementInfo" />
    <div v-for="(item, prop) in list" :key="prop">
      <div
        class="list-item"
        v-if="item.type == sortvalue || sortvalue == 'All'"
      >
        <span class="budget-comment" :class="[classIconArrow[item.type]]">
          {{ item.comment }}
        </span>
        <span class="budget-value"> {{ item.value }} </span>

        <el-button
          type="danger"
          size="mini"
          @click="
            (centerDialogVisible = true),
              (centerDialogVisibleID = item.id),
              (comment = item.comment)
          "
          >Delete
        </el-button>
      </div>
    </div>
    <el-dialog
      title="Warning"
      :visible.sync="centerDialogVisible"
      width="30%"
      center
    >
      <span> {{ comment }} </span>
      <span slot="footer" class="dialog-footer">
        <el-button @click="centerDialogVisible = false">Cancel</el-button>
        <el-button
          type="primary"
          @click="
            (centerDialogVisible = false), deleteThisItem(centerDialogVisibleID)
          "
          >Confirm
        </el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import SortElements from "./SortElements.vue";
export default {
  name: "BudgetListItem",
  components: {
    SortElements,
  },
  data: () => ({
    sortvalue: "All",
    centerDialogVisible: false,
    comment: "",
    centerDialogVisibleID: "",
    classIconArrow: {
      INCOME: "el-icon-top",
      OUTCOME: "el-icon-bottom",
    },
  }),
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  methods: {
    deleteThisItem(item) {
      this.$emit("deleteThisItem", item);
    },
    sortElementInfo(value) {
      if (value != undefined) {
        this.sortvalue = value;
      } else {
        this.sortvalue = "All";
      }
    },
  },
  computed: {
    display() {
      return "displayNone";
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
.display {
  display: flex;
}
.displayNone {
  display: none;
}
</style>
