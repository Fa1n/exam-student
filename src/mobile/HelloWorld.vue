<template>
      <el-row>
        <el-carousel :interval="5000" arrow="always" type="card">
          <el-carousel-item >
            <img src="@/assets/carousel/1.png" class="carousel-img">
          </el-carousel-item>
          <el-carousel-item >
            <img src="@/assets/carousel/2.png" class="carousel-img">
          </el-carousel-item>
          <el-carousel-item >
            <img src="@/assets/carousel/3.png" class="carousel-img">
          </el-carousel-item>
          <el-carousel-item >
            <img src="@/assets/carousel/4.png" class="carousel-img">
          </el-carousel-item>
        </el-carousel>
      </el-row>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'HelloWorld,I am mobile'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .mobile{
    font-size: 30px;
  }
</style>
