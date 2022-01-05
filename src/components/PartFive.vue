<template>
  <div :class="partFive">
    <h3 class="text-top">工作经验</h3>
    <p>
      <a href="javascript:void(0)">成都乐动信息技术有限公司</a>
      <span class="text-small">| 2018/06- 2019/02</span>
    </p>
    <p class="text-small">项目工作内容：</p>
    <p class="text-small">&emsp;1. 开发的app活动，在活动期间共计有30万的参与量</p>
    <p class="text-small">&emsp;2. 使用vue框架共计开发了10多个活动</p>
    <p class="text-small">&emsp;3. 维护公司官网以及开发一些静态H5页面</p>
    <p style="margin-top:10px;">
      <a href="javascript:void(0)">广州多益网络有限公司</a>
      <span class="text-small">| 2019/05- 2020/03</span>
    </p>
    <p class="text-small">项目工作内容：</p>
    <p class="text-small">&emsp;1. 开发游戏社区移动端</p>
    <p class="text-small">&emsp;2. 内部管理系统内部的一些常规流程、审核、申报、考核等功能的维护和修改，以及一些新增功能的开发（在家办公效能考核等）</p>
    <p style="margin-top:10px;">
      <a href="javascript:void(0)">海南安迈云网络技术有限公司</a>
      <span class="text-small">| 2020/06- 2022/01</span>
    </p>
    <p class="text-small">项目工作内容：</p>
    <p class="text-small">&emsp;1. APP及h5功能需求的迭代</p>
    <p class="text-small">&emsp;2. 使用Vue+TS开发并维护商品管理后台</p>
  </div>
</template>

<script>
export default {
  name: "partFive",
  data() {
    return {
      partFive: "part-five",
      curWidth: 0
    };
  },
  beforeMount() {
    this.curWidth = document.documentElement.clientWidth || document.body.clientWidth;
    if(this.curWidth < 1600) {
      this.partFive = "part-five-responsive"
    }
  }
};
</script>

<style scoped>
a {
  color: deepskyblue;
}
a:hover {
  color: rgb(118, 190, 248);
}
.part-five {
  width: 100%;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  opacity: 0.8;
  background: #18202d;
}
.part-five-responsive {
  width: 100%;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  opacity: 0.8;
  background: #18202d;
}
.text-center {
  text-align: center;
}
.text-small {
  font-size: 0.9em;
  color: rgb(253, 239, 239);
}
</style>
