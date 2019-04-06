<template>
  <div class="home">
    <el-container>
      <el-aside :style="leftWidth">
        <el-row class="tac" >
          <el-col :span="24">
            <div class="logo"></div>
            <el-menu
              default-active="2"
              :collapse="isCollapse"
              class="el-menu-vertical-demo"
              @open="handleOpen"
              @close="handleClose"
              background-color="#545c64"
              text-color="#fff"
              active-text-color="#ffd04b"
            >
              <el-submenu index="1">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>用户管理</span>
                </template>
                <el-menu-item-group>
                  <el-menu-item index="1-1"> <i class="el-icon-menu"></i>用户列表</el-menu-item>
                  <el-menu-item index="1-2"> <i class="el-icon-menu"></i>管理用户</el-menu-item>
                  <el-menu-item index="1-3"> <i class="el-icon-menu"></i>实时状况</el-menu-item>
                </el-menu-item-group>
              </el-submenu>
              <el-submenu index="2">
                <template slot="title">
                  <i class="el-icon-location"></i>
                  <span>用户管理</span>
                </template>
                <el-menu-item-group>
                  <el-menu-item index="2-1"> <i class="el-icon-menu"></i>列表1</el-menu-item>
                  <el-menu-item index="2-2"> <i class="el-icon-menu"></i>列表2</el-menu-item>
                  <el-menu-item index="2-3"> <i class="el-icon-menu"></i>列表3</el-menu-item>
                </el-menu-item-group>
              </el-submenu>
            </el-menu>
          </el-col>
        </el-row>
      </el-aside>
      <el-container>
        <!-- hearder 部分 -->
        <el-header>
          <i class="myicon myicon-menu" @click="toogleCollapse"></i>
          <div class="system-title">
            电商后台管理系统
          </div>
          <div class="system-button">
            你好，xxx
            <el-button
              type="text"
              style="color:orange"
              @click="logout"
            >退出</el-button>
          </div>
        </el-header>
        <el-main>
          Main
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import { getUserList } from "@/api";
export default {
  data() {
    return {
      id: "",
      isCollapse: false,
      leftWidth:"width:200px;transition:all 0.6s ease"
    };
  },
  created() {
    this.id = localStorage.getItem("mytoken");
    this.getUserList();
  },
  methods: {
    toogleCollapse(){
      // 切换isCollapse状态
      this.isCollapse=!this.isCollapse
      // 根据isCollapse的状态切换顶部图片一起
      this.leftWidth=!this.isCollapse?"width:200px;transition:all 0.6s ease":"width:64px;transition:all 0.6s ease"
      
    },
    logout(){
      localStorage.removeItem("mytocken")
      console.log(1);
      this.$router.push({name:"Login"})
      
    },
    getUserList() {
      // eslint-disable-next-line no-redeclare
      let params = { params: { query: "", pagenum: 1, pagesize: 1 } };
      getUserList(params).then(res => {
        console.log(res);
      });
    },
    handleOpen(key, keyPath) {
      console.log(key, keyPath);
    },
    handleClose(key, keyPath) {
      console.log(key, keyPath);
    }
  }
};
</script>

<style  scoped>
.home {
  width: 100%;
  height: 100%;
}
.el-menu-vertical-demo:not(.el-menu--collapse) {
    width: 200px;
  }
.myicon {
  float: left;
  padding-left: 10px;
  padding-top: 10px;
  font-size: 40px;
  margin: 0 auto;
  color: #ccc;
}
.system-title {
  font-size: 25px !important;
  line-height: initial;
  height: 60px;
  line-height: 60px;
}
.system-button {
  position: absolute;
  right: 20px;
  top: 0;
  height: 60px;
  font-size: 18px;
}
.logo {
  height: 60px;
  background: url(../assets/logo.png) no-repeat;
  background-size: cover;
  background-color: #989898;
}
.el-header,
.el-footer {
  background-color: #b3c0d1;
  color: #333;
  text-align: center;
  line-height: 60px;
}
.el-aside {
  background-color: #d3dce6;
  color: #333;
  text-align: center;
  height: 1000px;
  line-height: 100%;
}

.el-main {
  background-color: #e9eef3;
  color: #333;
  text-align: center;
  line-height: 160px;
}

body > .el-container {
  margin-bottom: 40px;
}

.el-container:nth-child(5) .el-aside,
.el-container:nth-child(6) .el-aside {
  line-height: 260px;
}

.el-container:nth-child(7) .el-aside {
  line-height: 320px;
}
</style>
