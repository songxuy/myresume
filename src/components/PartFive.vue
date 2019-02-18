<template>
  <div :class="partFive">
    <h3 class="text-center text-top">工作经验</h3>
    <p>
      <a href="javascript:void(0)">成都乐动信息技术有限公司</a>
      <span class="text-small">| 2018/06- 2019/01</span>
    </p>
    <p class="text-small">工作内容：通过vue框架编写前端页面调接口 通过express+node编写活动接口 编写一些静态H5页面 开发过其他的官网…</p>
    <p class="text-small">项目成就：</p>
    <p class="text-small">&emsp;1. 开发的app活动，在活动期间共计有30万的参与量</p>
    <p class="text-small">&emsp;2. 使用vue框架共计开发了20多个活动</p>
    <p class="text-small">&emsp;3. 维护公司官网  以及开发一些静态H5页面</p>
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
  height: 310px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
}
.part-five-responsive {
  width: 100%;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
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