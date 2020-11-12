<template>
  <div class="goods-item">
    <img :src="goodsItem.show.img" alt="" class="goods-img" />
    <div class="neirong">
      <p class="title">{{ goodsItem.title }}</p>
      <p class="content">
        <span class="price"
          >￥<span class="qian">{{ priceF }}</span
          >{{ priceL }}</span
        ><img
          src="~assets/img/home/shoucang.png"
          alt=""
          class="shoucangimg"
          width="14px"
        /><span class="cfav">{{ goodsItem.cfav }}</span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    goodsItem: {
      type: Object,
      default() {
        return [];
      },
    },
  },
  data() {
    return {};
  },
  computed: {
    priceF() {
      var ab = this.goodsItem.price;
      var ab_str = parseInt(ab.toString().split("."));
      return ab_str;
    },
    priceL() {
      var ab = this.goodsItem.price;
      var ab_str = ab.substring(ab.indexOf("."), ab.indexOf(".") + 3);
      return ab_str;
    },
  },
  methods: {
    //   shoucang(index){
    //       document.getElementsByClassName('shoucangimg')[index].setAttribute("src", "./static/img/home/shoucangsucce.png")
    //   }
  },
};
</script>
<style scoped>
.goods-item .neirong{
    padding: 0.2rem 0.5rem;
}
.goods-item .title {
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
}
.goods-img {
  width: 100%;
  
}
.goods-item .content {
  display: flex;
  align-items: center;
}
.goods-item .content img{
    margin-right: 2px;
}
.goods-item .content .price {
  color: var(--color-goods-text);
  margin-right: 0.5rem;
}
.goods-item .content .price .qian {
  font-size: 20px;
}
</style>