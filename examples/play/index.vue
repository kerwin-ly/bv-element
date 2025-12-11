<template>
  <section style="height: 2000px;">
    <el-dialog title="提示" :visible.sync="dialogVisible" width="30%" :before-close="handleClose" :lock-scroll="false">
      <div class="box" style="display: flex; justify-content: center; align-items: center;">
        <el-select v-model="value" placeholder="请输入关键词" style="height: 600px;">
          <el-option v-for="item in options" :key="item" :label="item" :value="item">
          </el-option>
        </el-select>
      </div>
    </el-dialog>
    <div style="margin-top: 500px; text-align: center;">
      <el-select v-model="value" placeholder="请输入关键词" style="height: 600px;">
        <el-option v-for="item in options" :key="item" :label="item" :value="item">
        </el-option>
      </el-select>
      <el-button type="primary" @click="dialogVisible = true">show dialog</el-button>
    </div>

    <div style="margin-top: 40px; padding: 20px; text-align: center; border: 1px dashed #dcdfe6;">
      <h4 style="margin-bottom: 16px;">before-change 示例</h4>
      <div style="margin-bottom: 12px;">
        <span style="margin-right: 8px;">开启拦截确认：</span>
        <el-switch v-model="guardEnabled"></el-switch>
      </div>
      <el-select
        v-model="guardValue"
        placeholder="选择州名"
        style="width: 260px;"
        :before-change="handlePreChange">
        <el-option v-for="item in options" :key="item" :label="item" :value="item"></el-option>
      </el-select>
      <div style="margin-top: 10px; color: #909399;">{{ beforeChangeMsg }}</div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.box {
  margin-top: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  border: 1px solid red;
  height: 800px;
}
</style>
<script>
import select from '../../packages/select/src/select.vue';
export default {
  components: { select },
  data() {
    return {
      dialogVisible: false,
      value: [],
      guardValue: '',
      guardEnabled: true,
      beforeChangeMsg: '',
      list: [],
      loading: false,
      options: ["Alabama", "Alaska", "Arizona",
        "Arkansas", "California", "Colorado",
        "Connecticut", "Delaware", "Florida",
        "Georgia", "Hawaii", "Idaho", "Illinois",
        "Indiana", "Iowa", "Kansas", "Kentucky",
        "Louisiana", "Maine", "Maryland",
        "Massachusetts", "Michigan", "Minnesota",
        "Mississippi", "Missouri", "Montana",
        "Nebraska", "Nevada", "New Hampshire",
        "New Jersey", "New Mexico", "New York",
        "North Carolina", "North Dakota", "Ohio",
        "Oklahoma", "Oregon", "Pennsylvania",
        "Rhode Island", "South Carolina",
        "South Dakota", "Tennessee", "Texas",
        "Utah", "Vermont", "Virginia",
        "Washington", "West Virginia", "Wisconsin",
        "Wyoming"]
    }
  },
  mounted() {
    document.body.style.zoom = 0.7;
  },
  methods: {
    handlePreChange(val) {
      if (!this.guardEnabled) {
        this.beforeChangeMsg = `未拦截，切换到 ${val}`;
        return true;
      }
      const allowed = window.confirm(`是否切换到 ${val} ?`);
      this.beforeChangeMsg = allowed ? `已允许切换到 ${val}` : `已阻止切换到 ${val}`;
      return allowed;
    },
    remoteMethod(query) {
      if (query !== '') {
        this.loading = true;
        setTimeout(() => {
          this.loading = false;
          this.options = this.list.filter(item => {
            return item.label.toLowerCase()
              .indexOf(query.toLowerCase()) > -1;
          });
        }, 200);
      } else {
        this.options = [];
      }
    }
  }
}
</script>
