<template>
  <div class="index" ><!--:style="{backgroundImage:`url(${loginBackgroundImg})`}"-->
    <el-container class="indexMain">


      <el-aside :width="sideWidth+'px'" class="elAsideHome">
        <img src="../assets/logo.png" style="width: 20px; position: relative; top: 5px; margin-right: 5px">
        <b style="color: red" v-show="logoTextShow">Dream后台管理系统</b>
        <el-menu :default-openeds="['1', '3']" class="elMenuHome" :collapse-transition="false" :collapse="isCollapse">
          <el-submenu index="1">
            <template slot="title"><i class="el-icon-message"></i>导航一</template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="1-1">选项1</el-menu-item>
              <el-menu-item index="1-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="1-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="1-4">
              <template slot="title">选项4</template>
              <el-menu-item index="1-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title"><i class="el-icon-menu"></i>导航二</template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="2-1">选项1</el-menu-item>
              <el-menu-item index="2-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="2-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="2-4">
              <template slot="title">选项4</template>
              <el-menu-item index="2-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="3">
            <template slot="title"><i class="el-icon-setting"></i>导航三</template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="3-1">选项1</el-menu-item>
              <el-menu-item index="3-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="3-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="3-4">
              <template slot="title">选项4</template>
              <el-menu-item index="3-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
        </el-menu>
      </el-aside>
      <span :class="collapseBtnClass" style="cursor: pointer" @click="collapse"></span>
      <el-container>
        <el-header style="text-align: right; font-size: 12px">
          <el-dropdown>
            <i class="el-icon-setting" style="font-size: 25px; margin-top: 15px;color: #42b983"></i>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>个人中心</el-dropdown-item>
              <el-dropdown-item>设置</el-dropdown-item>
              <el-dropdown-item>注销登录</el-dropdown-item>
              <el-dropdown-item @click.native="setBackgroundImg()">注更主题</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-header>

        <el-main>
          <el-table :data="tableData">
            <el-table-column prop="date" label="日期" width="140">
            </el-table-column>
            <el-table-column prop="name" label="姓名" width="120">
            </el-table-column>
            <el-table-column prop="address" label="地址">
            </el-table-column>
          </el-table>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import backgroundImg1 from "../assets/images/background/c586cac74b474b5ea5458a046e8b14c0.jpg";
import backgroundImg2 from "../assets/images/background/c9d3deb2880411ebb6edd017c2d2eca2.jpg";
import backgroundImg3 from "../assets/images/background/c8bfcd9f880411ebb6edd017c2d2eca2.jpg";
import backgroundImg4 from "../assets/images/background/wallhaven-qzmzvd_1920x1080.png";
export default {
  name: "home",
  data() {
    const item = {
      date: '2016-05-02',
      name: '王小虎',
      address: '上海市普陀区金沙江路 1518 弄'
    };
    return {
      tableData: Array(20).fill(item),
      imgIndex: 0,
      loginBackgroundImg: backgroundImg1,
      imgList: [{"id": 0, "url": backgroundImg1}, {"id": 1, "url": backgroundImg2}, {
        "id": 2,
        "url": backgroundImg3
      }, {"id": 3, "url": backgroundImg4}],
      collapseBtnClass: "el-icon-s-fold",
      logoTextShow: true,
      //默认宽度200
      sideWidth: 200,
    }
  }, methods: {
    //复制背景图
    setBackgroundImg() {
      this.imgIndex = this.imgIndex + 1;
      if (this.imgIndex > this.imgList.length - 1) {
        this.imgIndex = 0;
      }
      this.loginBackgroundImg = this.imgList[this.imgIndex].url;
      console.log(this.imgIndex);
    },//点击收缩按钮触发
    collapse(){
      //collapse为false时展开，为true时折叠。
      this.isCollapse = !this.isCollapse
      //折叠时
      if(this.isCollapse){
        //折叠时宽度为64
        this.sideWidth = 100
        //变换图标样式
        this.collapseBtnClass = 'el-icon-s-unfold'
        //折叠时不展示名称“ML后台管理系统”
        this.logoTextShow = false
        //展开时
      }else{
        //展开时宽度为200
        this.sideWidth = 200
        //变换图标样式
        this.collapseBtnClass = 'el-icon-s-fold'
        //展开时展示名称“ML后台管理系统”
        this.logoTextShow = true
      }
    }
  }
}
</script>

<style>
.index{
  position : absolute;
  width : 100%;
  height : 100%;
  /* 加载背景图 */
//background-image: url("../assets/images/background/c586cac74b474b5ea5458a046e8b14c0.jpg");
  /* 背景图垂直、水平均居中 */
  background-position: center center;
  /* 背景图不平铺 */
  background-repeat: no-repeat;
  /* 当内容高度大于图片高度时，背景图像的位置相对于viewport固定 */
  background-attachment: fixed;
  /* 让背景图基于容器大小伸缩 */
  background-size: cover;
  /* 设置背景颜色，背景图加载过程中会显示背景色 */
//background-color: #464646;
}
.indexMain{
  height:100%
}
html,body{
  height: 100%;
}
.elAsideHome::-webkit-scrollbar {
  display: none;
}
.elAsideHome{
  height:100%;

}
.elMenuHome{
  height:100%;
  //border-right: ;
  border-right:none !important;
}
</style>