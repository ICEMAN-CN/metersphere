<template>
  <el-card class="table-card" v-loading="result.loading">
    <template v-slot:header>
      <span class="title">
        {{$t('api_test.home_page.failed_case_list.title')}}
      </span>
    </template>
    <el-table border :data="tableData" class="adjust-table table-content" height="300px">
      <el-table-column prop="sortIndex"  :label="$t('api_test.home_page.failed_case_list.table_coloum.index')" width="100" show-overflow-tooltip/>
      <el-table-column prop="caseName"  :label="$t('api_test.home_page.failed_case_list.table_coloum.case_name')" width="250" show-overflow-tooltip/>
      <el-table-column prop="testPlan"  :label="$t('api_test.home_page.failed_case_list.table_coloum.test_plan')" show-overflow-tooltip/>
      <el-table-column prop="failureTimes"  :label="$t('api_test.home_page.failed_case_list.table_coloum.failure_times')" width="100" show-overflow-tooltip/>
    </el-table>
  </el-card>
</template>

<script>
import {getCurrentProjectID} from "@/common/js/utils";

export default {
  name: "MsFailureTestCaseList",


  data() {
    return {
      result: {},
      tableData: [],
      loading: false
    }
  },

  methods: {
    search() {
      let projectID = getCurrentProjectID();
      this.result = this.$get("/api/faliureCaseAboutTestPlan/"+projectID+"/10", response => {
        this.tableData = response.data;
      });
    },
  },


  created() {
    this.search();
  },
  activated() {
    this.search();
  }
}
</script>

<style scoped>

.el-table {
  cursor:pointer;
}

</style>
