<template>
  <elCard class="form-card">
    <el-form
      :model="formData"
      ref="addItemForm"
      :rules="rules"
      label-position="top"
    >
      <el-form-item label="Type" prop="type">
        <el-select
          class="type-select"
          v-model="formData.type"
          placeholder="Choose type"
        >
          <el-option label="Income" value="INCOME" />
          <el-option label="Outcome" value="OUTCOME" />
        </el-select>
      </el-form-item>
      <el-form-item label="Comments" prop="comment">
        <el-input v-model="formData.comment"> </el-input>
      </el-form-item>
      <el-form-item label="Value" prop="value">
        <el-input v-model.number="formData.value"> </el-input>
      </el-form-item>
      <el-button type="primary" @click="onSubmit">Submit</el-button>
    </el-form>
  </elCard>
</template>

<script>
export default {
  name: "FormBudget",
  data: () => ({
    formData: {
      type: "INCOME",
      comment: "",
      value: 0,
    },
    rules: {
      type: [
        { required: true, message: "please select type", trigger: "blur" },
      ],
      comment: [
        { required: true, message: "please type something", trigger: "change" },
      ],
      value: [
        { required: true, message: "please entet amount", trigger: "blur" },
        { type: "number", message: "value must be a number", trigger: "blur" },
      ],
    },
  }),
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate((valid) => {
        if (valid) {
          this.$emit("submitForm", { ...this.formData });
          this.$refs.addItemForm.resetFields();
        }
      });
    },
  },
};
</script>

<style scoped>
.form-card {
  max-width: 500px;
  margin: auto;
  text-align: left;
}
.type-select {
  width: 100%;
}
</style>
