<template>
  <div class="goods-list">
    <goods-list-item
      v-for="(item, index) in goods"
      :key="index"
      :goodsItem="item"
    ></goods-list-item>
  </div>
</template>

<script>
import GoodsListItem from "./GoodsListItem.vue";
export default {
  props: {
    goods: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {};
  },
  components: {
    GoodsListItem,
  },
};
</script>
<style scoped>
.goods-list{
    display: flex;
    width: 100%;
    flex-wrap: wrap;
    background-color: #eee;
}
.goods-list>div{
    width: 47%;
    margin: 0.3rem;
    border-radius: 5px;
    background-color: #FFF;
    overflow: hidden;
}
</style>