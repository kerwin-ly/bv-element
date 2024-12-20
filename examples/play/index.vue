<template>
  <section>
    <div class="box">
      <el-select v-model="value" placeholder="请输入关键词">
        <el-option v-for="item in options" :key="item" :label="item" :value="item">
        </el-option>
      </el-select>
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
      value: [],
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
    document.body.style.zoom = 0.8;
  },
  methods: {
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
