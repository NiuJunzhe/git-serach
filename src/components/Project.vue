<template>
  <div>
    <el-dialog title="项目信息" :visible.sync="isShowDialog">
      {{project}}
    </el-dialog>
  </div>
</template>

<script>
    export default {
      name: "Project",
      props:['ProjectData'],
      data() {
          return {
             isShowDialog: false,
            project: {
              // id: '',
              // group: '',
              // artifactId: '',
            }
          }

      },
      methods: {
        showDialog() {
          this.isShowDialog = !this.isShowDialog;
        },
        getProject(val) {
          this.project = val;
        }
      }
    }
</script>

<style scoped>

</style>
