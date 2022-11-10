<template>
  <ElCard class="form-card">
    <ElForm :model="formData" ref="addItemForm" :rules="rules" lable-position="top">
      <ElFormItem label="Type" prop="type">
        <ElSelect class="type-select" v-model="formData.type" placeholder="Choose type...">
          <ElOption lable="Income" value="INCOME" />
          <ElOption lable="Outcome" value="OUTCOME" />
        </ElSelect>
      </ElFormItem>
      <ElFormItem label="Comments" prop="comment">
        <ElInput v-model="formData.comment" />
      </ElFormItem>
      <ElFormItem label="Value" prop="value">
        <ElInput v-model.number="formData.value" />
      </ElFormItem>
      <ElButton @click="onSubmit" type="primary">Submit</ElButton>
    </ElForm>
  </ElCard>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Form",
  data ()  {
    var checkAge = (rule, value, callback) => {
        rule = this.formData.type;
        if ((!value) || (rule === 'OUTCOME' && value > 0)) {
          return callback(new Error('Please input number different from 0'));
        }
        setTimeout(() => {
          if (!Number.isInteger(value)) {
            callback(new Error('Please input digits'));
          } else {
              callback();
            }
        }, 1000);
      };
    return {formData: {
      type: "INCOME",
      comment: "",
      value: null
    },

    rules: {
      type: [
        { required: true, message: "Please select type", trigger: "blur" }
      ],
      comment: [
        { required: true, message: "Please input comment", trigger: "change" }
      ],
      value: [
        { validator: checkAge, trigger: 'blur' },
        {required: true}
      ]

    },
  }
  },
  methods: {
    onSubmit() {
      this.$refs.addItemForm.validate(valid => {
        if (valid) {
          this.$emit("submitForm", { ...this.formData });
          this.$refs.addItemForm.resetFields();
        }
      });
    }
  },

};
</script>

<style scoped>
.form-card {
  max-width: 500px;
  margin: auto;
  background-color: #8df4f750;
  border-radius: 40px;
}

.type-select {
  width: 100%;
}
</style>