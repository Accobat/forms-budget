<template>
  <div class="budget-list-wrap">
    <ElSelect class="type-select" placeholder="Choose type..." v-model="formSelect.type">
      <ElOption lable="All" value="ALL" />
      <ElOption lable="Income" value="INCOME" />
      <ElOption lable="Outcome" value="OUTCOME" />
    </ElSelect>
    <ElCard >
      <div class="header">Budget List</div>
      <template v-if="!isEmpty && formSelect.type === 'INCOME'">
        <div class="list-item" v-for="(item, prop) in list" :key="prop">
          <i class="el-icon-top" v-show="item.type === 'INCOME'"></i>
          <span class="budget-comment" v-show="item.type === 'INCOME'">{{ item.comment }}</span>
          <span class="budget-value-top" v-show="item.type === 'INCOME'">{{ item.value }}</span>
          <template>
            <el-popconfirm
              title="Are you sure to delete this?"
              @confirm="deleteItem(item.id)">
            <el-button slot="reference" type="danger" size="mini" v-show="item.type === 'INCOME'">Delete</el-button>
            </el-popconfirm>
            </template>
                  </div>
                  </template>
                  <template v-else-if="!isEmpty && formSelect.type === 'OUTCOME'">
                    <div class="list-item" v-for="(item, prop) in list" :key="prop">
                      <i class="el-icon-bottom" v-show="item.type === 'OUTCOME'"></i>
                      <span class="budget-comment" v-show="item.type === 'OUTCOME'">{{ item.comment }}</span>
                      <span class="budget-value-bottom" v-show="item.type === 'OUTCOME'">{{ item.value }}</span>
                      <template>
                        <el-popconfirm
                          title="Are you sure to delete this?"
                          @confirm="deleteItem(item.id)">
                          <el-button slot="reference" type="danger" size="mini" v-show="item.type === 'OUTCOME'">Delete</el-button>
                        </el-popconfirm>
                      </template>
                    </div>
                  </template>
                  <template v-else-if="!isEmpty && formSelect.type === 'ALL'">
                    <div class="list-item" v-for="(item, prop) in list" :key="prop">
                      <i class="el-icon-top" v-show="item.type === 'INCOME'" ></i>
                      <span class="budget-comment" v-show="item.value >= 0">{{ item.comment }}</span>
                      <span class="budget-value-top" v-show="item.value >= 0">{{ item.value }}</span>
                      <template>
                        <el-popconfirm
                          title="Are you sure to delete this?"
                          @confirm="deleteItem(item.id)">
                          <el-button slot="reference" type="danger" size="mini" v-show="item.value >= 0">Delete</el-button>
                        </el-popconfirm>
                      </template>
                    </div>
                    <div class="list-item" v-for="(item, prop) in list" :key="prop">
                      <i class="el-icon-bottom" v-show="item.type === 'OUTCOME'"></i>
                      <span class="budget-comment" v-show="item.value < 0">{{ item.comment }}</span>
                      <span class="budget-value-bottom" v-show="item.value < 0">{{ item.value }}</span>
                      <template>
                        <el-popconfirm
                          title="Are you sure to delete this?"
                          @confirm="deleteItem(item.id)">
                          <el-button slot="reference" type="danger" size="mini" v-show="item.value < 0">Delete</el-button>
                        </el-popconfirm>
                      </template>
                    </div>
                  </template>

      <ElAlert v-else type="info" :title="emptyTitle" :closable="false" />
    </ElCard>
  </div>
</template>

<script>
export default {
  name: "BudgetList",
  props: {
    list: {
      type: Object,
      default: () => ({})
    }
  },
  data: () => ({
    emptyTitle: "Empty List",
    formSelect: {
      type: "ALL"
    },
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    }
  },
  methods: {
    deleteItem(id) {
      this.$emit("deleteItem", id);
    },

  }
};
</script>

<style scoped>
.budget-list-wrap {
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

.budget-value-top {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
  color: green;

}

.budget-value-bottom {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
  color: red;
}

.type-select {
  width: 440px;
}

.el-card {
  background-color: #8df4f750;
  border-radius: 40px;
}

.header {
 padding-bottom: 20px;
 border-bottom:1px solid black;
 box-sizing:border-box
}
</style>

