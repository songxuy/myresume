<template>
  <div :class="partSix">
    <h3 class="text-center">编程技能</h3>
    <p class="font-small"><span class="font-bold">前端：</span>HTML5、CSS/SASS/LESS、JS/TS、Vue、React……</p>
    <!-- <p class="font-small"><span class="font-bold">后端：</span>NodeJS</p> -->
    <p class="font-small"><span class="font-bold">其他：</span>Canvas、Webpack</p>
  </div>
</template>

<script>
export default {
  name: "partSix",
  data() {
    return {
      partSix: "part-six",
      curWidth: 0
    };
  },
  beforeMount() {
    this.curWidth = document.documentElement.clientWidth || document.body.clientWidth;
    if(this.curWidth < 1600) {
      this.partSix = "part-six-responsive"
    }
  }
};
</script>

<style scoped>
.part-six {
  width: 100%;
  height: 310px;
  border: 20px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  opacity: 0.8;
  background: #18202d;
}
.part-six-responsive {
  width: 100%;
  border: 20px solid transparent;
  border-image: url("~@/./assets/img/border_image.png") 30 30 stretch;
  opacity: 0.8;
  background: #18202d;
}
.text-center {
  text-align: center;
}
.font-small {
  font-size: .9em;
}
.font-bold {
  font-weight: bold;
  color: deepskyblue;
}
</style>
