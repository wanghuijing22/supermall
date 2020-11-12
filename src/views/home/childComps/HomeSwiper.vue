<template>
  <mt-swipe :auto="4000" >
    <mt-swipe-item  v-for="(item, index) in banners" :key="index">
      <a :href="item.link">
        <img :src="item.image" alt="" />
      </a>
    </mt-swipe-item>
  </mt-swipe>
</template>

<script>
export default {
  props: {
    banners: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {};
  },
};
</script>
<style scoped>
.mint-swipe-items-wrap{
  background-color: rosybrown;
  height: 50px;
}
.mint-swipe{
  height: 200px;
}
.mint-swipe img{
  width: 100%;
  height: 100%;
}
</style>