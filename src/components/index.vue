<template>
  <div>
    <div><h1>Jar收集工具</h1></div>
    <div>
      <el-form :inline="true" :model="formInline" class="demo-form-inline">
        <el-form-item label="Jar分组">
          <el-input v-model="formInline.groupId"></el-input>
        </el-form-item>
        <el-form-item label="Jar坐标">
          <el-input v-model="formInline.artifactId"></el-input>
        </el-form-item>
        <el-form-item label="Jar坐标">
          <el-input v-model="formInline.version"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button type="primary" @click="onSubmit">查询</el-button>
        </el-form-item>
      </el-form>
    </div>
    <div>
      <el-table :data="tableData.slice((currentPage-1)*pageSize,currentPage*pageSize)" :border="true">
        <el-table-column type="index" width="50" label="序号"></el-table-column>
        <el-table-column label="项目坐标" :show-overflow-tooltip="true">
          <template slot-scope="scope">
            <div @click="showDialog(scope.row)">{{scope.row.pomArtifactId}}</div>
          </template>
        </el-table-column>
        <el-table-column prop="pomVersion" label="项目版本" :show-overflow-tooltip= "true"></el-table-column>
        <el-table-column prop="jarGroupId" label="jar分组" :show-overflow-tooltip="true"></el-table-column>
        <el-table-column prop="jarArtifactId" label="jar坐标" :show-overflow-tooltip="true"></el-table-column>
        <el-table-column prop="jarVersion" label="jar版本" :show-overflow-tooltip="true"></el-table-column>
      </el-table>
      <el-pagination
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-size="pageSize"
        layout="total, prev, pager, next, jumper"
        :total="tableData.length"
        :page-count="tableData.length/pageSize">
      </el-pagination>
    </div>
    <div>
      <project-item ref="projectItem" :project-data="tableData"></project-item>
    </div>
  </div>
</template>
<script>
  import ProjectItem from './Project.vue';
export default {
  components: {
    ProjectItem
  },
  data() {
    return {
      formInline: {
        groupId: '',
        artifactId: '',
        version: ''
      },
      tableData: [{
        projectId: '',
        pomArtifactId: 'pom坐标',
        pomVersion: 'pom版本pom版本pom版本pom版本pom版本pom版本pom版本pom版本pom版本pom版本pom版本pom版本',
        jarGroupId: 'jar分组',
        jarArtifactId: 'jar坐标',
        jarVersion: 'jar版本',
      }, {
        projectId: '',
        pomArtifactId: 'pom坐标',
        pomVersion: 'pom版本',
        jarGroupId: 'jar分组',
        jarArtifactId: 'jar坐标',
        jarVersion: 'jar版本',
      }],
      currentPage: 1, //当前页
      pageSize: 10, //当前显示条数
    }
  },
  methods: {
    onSubmit() {
      alert(this.formInline.version+this.formInline.artifactId);
    },
    handleCurrentChange(val) {
      this.currentPage = val
    },
    showDialog(val) {
      this.$refs.projectItem.showDialog()
      this.$refs.projectItem.getProject(val)

    }
  }
}
</script>
