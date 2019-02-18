<template>
  <div class="app" id="app">
     <div class="banner">
     <!--  <img class="hidden-md-only hidden-lg-only hidden-xl-only" :src="bannerXSSM" alt="banner 图">
      <img class="hidden-xs-only hidden-sm-only hidden-lg-only hidden-xl-only" :src="bannerMD" alt="banner 图">
      <img class="hidden-xs-only hidden-sm-only hidden-md-only" :src="bannerLGXL" alt="banner 图">-->
    </div> 
    <!-- 第一行 -->
    <el-row>
      <el-col :xs="24" :sm="24" :md="6" :lg="7" :xl="6" class="part">
        <router-view name="PartOne"/>
      </el-col>
      <el-col :xs="24" :sm="24" :md="10" :lg="10" :xl="6" class="part">
        <router-view name="PartTwo"/>
      </el-col>
      <el-col :xs="24" :sm="24" :md="8" :lg="7" :xl="12" class="part">
        <router-view name="PartThree"/>
      </el-col>
    </el-row>
    <!-- 第二行 -->
    <el-row>
      <el-col :xs="24" :sm="24" :md="8" :lg="8" :xl="8" class="part">
        <router-view name="PartFour"/>
      </el-col>
      <el-col :xs="24" :sm="24" :md="8" :lg="8" :xl="8" class="part">
        <router-view name="PartFive"/>
      </el-col>
      <el-col :xs="24" :sm="24" :md="4" :lg="4" :xl="4" class="part">
        <router-view name="PartSix"/>
      </el-col>
      <el-col :xs="24" :sm="24" :md="4" :lg="4" :xl="4" class="part">
        <router-view name="PartSeven"/>
      </el-col>
    </el-row>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      bannerXSSM: require("./assets/img/banner_640.png"),
      bannerMD: require("./assets/img/banner_1000.png"),
      bannerLGXL: require("./assets/img/banner.png"),
    };
  }
};
</script>

<style>
.app{
  position: relative;
  width:100%;
  color:#fff;
}
.banner {
  background: url(https://sp-webfront.skypixel.com/skypixel/v2/public/website/assets/1535027674204-f6eca6369ec03e70262b58b0e25cda7b.jpg);
  background-size: cover;
  position: fixed;
  top: -20px;
  left: -20px;
  right: -20px;
  bottom: -20px;
  color: #fff;
  width: 100%;
  -webkit-animation: move 50s infinite;
  animation: move 50s infinite;
}
.part {
  padding: 5px;
}
/* .banner img {
  width: 100%;
  height: 80px;
} */
.BMap_cpyCtrl, .BMap_noprint, .anchorBL {
  display: none !important;
}
@keyframes move {
 0% {
  background-position: 0 0;
 }
 50% {
  background-position: 100% 0;
 }
}
</style>