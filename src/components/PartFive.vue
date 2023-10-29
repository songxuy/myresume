<!--
 * @Author: songxuyuan 541046145@qq.com
 * @Date: 2021-08-10 20:50:36
 * @LastEditors: songxuyuan 541046145@qq.com
 * @LastEditTime: 2023-10-29 22:39:39
 * @FilePath: \myresume\src\components\PartFive.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <div :class="partFive">
    <h3 class="text-top">工作经验</h3>
    <!-- <p>
      <a href="javascript:void(0)">成都乐动信息技术有限公司</a>
      <span class="text-small">| 2018/06- 2019/02</span>
    </p>
    <p class="text-small">项目工作内容：</p>
    <p class="text-small">&emsp;1. 开发的app活动，在活动期间共计有30万的参与量</p>
    <p class="text-small">&emsp;2. 使用vue框架共计开发了10多个活动</p>
    <p class="text-small">&emsp;3. 维护公司官网以及开发一些静态H5页面</p> -->
    <p style="margin-top:10px;">
      <a href="javascript:void(0)">广州多益网络有限公司</a>
      <span class="text-small">| 2019/05- 2020/03</span>
    </p>
    <p class="text-small">项目工作内容：</p>
    <p class="text-small">&emsp;1. 开发游戏社区移动端</p>
    <p class="text-small">&emsp;2. 内部管理系统内部的一些常规流程、审核、申报、考核等功能的维护和修改，以及一些新增功能的开发（在家办公效能考核等）</p>
    <p style="margin-top:10px;">
      <a href="javascript:void(0)">海南安迈云网络技术有限公司</a>
      <span class="text-small">| 2020/06- 2022/02</span>
    </p>
    <p class="text-small">项目工作内容：</p>
    <p class="text-small">&emsp;1. APP及h5功能需求的迭代</p>
    <p class="text-small">&emsp;2. 使用Vue+TS开发并维护商品管理后台</p>
    <p style="margin-top:10px;">
      <a href="javascript:void(0)">华雁智能科技股份有限公司</a>
      <span class="text-small">| 2022/03- 2023/06</span>
    </p>
    <p class="text-small">项目工作内容：</p>
    <p class="text-small">&emsp;1. 负责低代码平台功能的迭代开发(权限管理、主题、导航、工作台、组件与平台的交互等)</p>
    <p class="text-small">&emsp;2. 基于平台流程的组件及导航开发</p>
    <p class="text-small">&emsp;3. 项目发布基座开发及迭代</p>
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
