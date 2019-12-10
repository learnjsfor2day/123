/announcement/
<template>
  <el-card class="box-card">
    <div slot="header" class="clearfix">
      <span style="font-weight: bold;font-size: 20px">Announcement</span>
      <!--<el-button style="float: right; padding: 3px 0" type="text">修改</el-button>-->
    </div>
    <div class="block">
      <el-timeline>
        <el-timeline-item timestamp="2019-11-07" placement="top">
          <el-card>
            <h4>Notice on Announcement of the Results of "The Librarian Book Review Season Seven Call for Activities in 2019"</h4>
            <p>Tom submitted on 2019-11-07</p>
          </el-card>
        </el-timeline-item>
        <el-timeline-item timestamp="2019-9-23" placement="top">
          <el-card>
            <h4>Library opens during National Day</h4>
            <p>Tom submitted on 2019-9-23</p>
          </el-card>
        </el-timeline-item>
        <el-timeline-item timestamp="2019-09-11" placement="top">
          <el-card>
            <h4>Library Mid-Autumn Festival Opening Notice</h4>
            <p>Tom submitted on 2019-09-11</p>
          </el-card>
        </el-timeline-item>
        <el-timeline-item timestamp="2019-07-01" placement="top">
          <el-card>
            <h4>Call for Librarian Book Reviews 2019</h4>
            <p>Tom submitted on 2019-07-01</p>
          </el-card>
        </el-timeline-item>
        <el-timeline-item timestamp="2019-06-24" placement="top">
          <el-card>
            <h4>2019 summer library opening notice</h4>
            <p>Tom submitted on 2019-06-24</p>
          </el-card>
        </el-timeline-item>
      </el-timeline>
    </div>
  </el-card>
</template>

<script>
  export default {
    name: 'UpdateCard'
  }
</script>

<style scoped>
  .box-card {
    margin-top: 5px;
    width: 988px;
    height: 1050px;
    text-align: left;
  }
</style>
