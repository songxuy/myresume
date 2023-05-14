<!--
 * @Author: songxuyuan 541046145@qq.com
 * @Date: 2021-08-10 20:50:36
 * @LastEditors: songxuyuan 541046145@qq.com
 * @LastEditTime: 2023-05-15 00:03:12
 * @FilePath: \myresume\src\components\PartOne.vue
 * @Description: 这是默认设置,请设置`customMade`, 打开koroFileHeader查看配置 进行设置: https://github.com/OBKoro1/koro1FileHeader/wiki/%E9%85%8D%E7%BD%AE
-->
<template>
  <div class="part-one">
    <img class="part-one-image" :src="headImage" alt="头像" style="margin-bottom:10px;">
    <p>姓&emsp;&emsp;名：宋旭缘</p>
    <p>学&emsp;&emsp;历：本科</p>
    <p>工作年限：3 年</p>
    <p>年&emsp;&emsp;龄：26</p>
    <p>联系电话：18096295110</p>
    <p>电子邮箱：541046145@qq.com</p>
    <p>博&emsp;&emsp;客：<a href="http://songxuy.github.io">blog</a></p>
    <p>GitHub：<a href="https://github.com/songxuy">SXY</a></p>
  </div>
</template>

<script>
export default {
  name: "partOne",
  data() {
    return {
      headImage: require('../assets/img/head12.jpg')
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
p {
  line-height: 30px;
}
.part-one {
  width: 100%;
  height: 500px;
  border: 40px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  background: #18202d;
  opacity: 0.8;
  padding-left: 10px;
}
.part-one-image {
  width: 150px;
  height: 150px;
}
</style>
