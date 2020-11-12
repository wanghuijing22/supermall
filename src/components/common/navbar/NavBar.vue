<template>
  <div class="nav-bar">
      <div class="left"><slot name="left"></slot></div>
      <div class="center"><slot name="center"></slot></div>
      <div class="right"><slot name="right"></slot></div>
  </div>
</template>

<script>
export default {
    name:'NavBar',
  data () {
    return {
    };
  },
}

</script>
<style scoped>
.nav-bar{
    height: 44px;
    line-height: 44px;
    display: flex;
    width: 100%;
}
.left,.right{
    width: 60px;
    /* background-color: seashell; */
}
.center{
    flex: 1;
}
</style>