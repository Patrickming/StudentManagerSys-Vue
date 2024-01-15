<template>
  <div>
    <el-menu
      style="border-top: 1px grey solid;"
      :collapse="collapse"
      class="aside"
      background-color="#304156"
      text-color="#fff"
      router
      >
      <el-menu-item index="dashboard" :class="{active: $route.name === '首页'}">
        <i class="iconfont icon-r-home" style="font-size: 26px;"></i>
        <span slot="title">首页</span>
      </el-menu-item>

      <el-menu-item index="course" v-if="level === 0" :class="{active: $route.name === '课程信息管理'}">
        <i class="iconfont icon-r-mark1" style="font-size: 26px;"></i>
        <span slot="title">课程信息管理</span>
      </el-menu-item>

      <el-menu-item index="timetable" :class="{active: $route.name === '课程表'}">
        <i class="iconfont icon-r-paper" style="font-size: 26px;"></i> 课程表管理
      </el-menu-item>

      <el-menu-item index="score" :class="{active: $route.name === '成绩信息管理'}">
        <i class="iconfont icon-r-yes" style="font-size: 24px;"></i> 
        <span slot="title"> 成绩信息管理</span>
      </el-menu-item>

      <el-menu-item index="analysis" :class="{active: $route.name === '成绩统计分析'}">
        <i class="iconfont icon-r-shield" style="font-size: 26px;"></i>
        <span slot="title">成绩统计分析</span>
      </el-menu-item>

      <el-submenu index="setting" v-if="level === 0">
        <template slot="title">
        <i class="iconfont icon-r-user2" style="font-size: 26px;"></i>
        <span>用户信息管理</span>
        </template>
          <el-menu-item-group>
            <el-menu-item index="student" :class="{active: $route.name === '学生用户'}">
              <i class="iconfont icon-r-user2" style="font-size: 26px;"></i>
              <span slot="title">学生用户</span>
            </el-menu-item>
          </el-menu-item-group>
        <el-menu-item-group>
          <el-menu-item index="teacher" :class="{active: $route.name === '教师用户'}">
            <i class="iconfont icon-r-user3" style="font-size: 26px;"></i>
            <span slot="title">教师用户</span>
          </el-menu-item>
        </el-menu-item-group>
        <el-menu-item-group>
          <el-menu-item index="admin" :class="{active: $route.name === '管理员用户'}">
              <i class="iconfont icon-r-user1" style="font-size: 26px;"></i>
            <span slot="title">管理员用户</span>
          </el-menu-item>
        </el-menu-item-group>
      </el-submenu>

      <el-menu-item index="account" v-if="level === 0" :class="{active: $route.name === '账号信息管理'}">
        <i class="iconfont icon-r-setting" style="font-size: 26px;"></i>
        <span slot="title">账号信息管理</span>
      </el-menu-item>
    </el-menu>
  </div>
</template>

<script>
export default {
    name: "Aside",
    data() {
        return {
            collapse: false,
            level: -1,
        };
    },
    methods: {
        isCollapse() {
            this.collapse = !this.collapse;
            this.$emit("collapse", this.collapse);
        },
    },
    mounted() {
        this.userInfo = JSON.parse(localStorage.userInfo);
        this.level = this.userInfo.level;
        
    },
};
</script>
<style scoped>
.el-submenu .el-menu-item {
    margin-left: 61px;
}
/*子导航栏时的样式*/
/deep/ .el-submenu .el-menu-item {
    min-width: 80px !important;
    width: 164px;
    height: 40px;
    margin-bottom: 5px !important;
    margin-left: 5px !important;
    line-height: 40px;
    text-align: center;
    border-radius: 55px;
}
/deep/ .el-menu-item-group__title {
    padding: 0;
}
.el-menu {
    border: 0;
    /*background-image: linear-gradient(#4777e7, rgba(90,139,255,0.68));*/
}

.active {
    background-color: #304156;
    color: rgb(64, 158, 255);
}
</style>
