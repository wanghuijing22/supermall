<!--  -->
<template>
  <tabbar>
      <!-- itemColor属性设置item的文字颜色 变成动态的 没有这个属性就使用默认 -->
      <tabbar-item path="/home" >
        <img src="~assets/img/shouye.svg" alt="" srcset="" slot="tabbarImg" />
        <img
          src="~assets/img/shouye-light.svg"
          alt=""
          srcset=""
          slot="tabbarImg-light"
        />
        <div slot="tabbarText">首页</div>
      </tabbar-item>
      <tabbar-item path="/category">
        <img src="~assets/img/fenlei.svg" alt="" srcset="" slot="tabbarImg" />
        <img
          src="~assets/img/fenlei-light.svg"
          alt=""
          srcset=""
          slot="tabbarImg-light"
        />
        <div slot="tabbarText">分类</div>
      </tabbar-item>
      <tabbar-item path="/cart">
        <img
          src="~assets/img/gouwuche.svg"
          alt=""
          srcset=""
          slot="tabbarImg"
        />
        <img
          src="~assets/img/gouwuche-light.svg"
          alt=""
          srcset=""
          slot="tabbarImg-light"
        />
        <div slot="tabbarText">购物车</div>
      </tabbar-item>
      <tabbar-item path="/profile">
        <img src="~assets/img/wode.svg" alt="" srcset="" slot="tabbarImg" />
        <img
          src="~assets/img/wode-light.svg"
          alt=""
          srcset=""
          slot="tabbarImg-light"
        />
        <div slot="tabbarText">我的</div>
      </tabbar-item>
    </tabbar>
</template>

<script>
import Tabbar from "components/common/tabbar/Tabbar.vue";
import TabbarItem from "components/common/tabbar/TabbarItems.vue";
export default {
  data () {
    return {
    };
  },
  components:{
      Tabbar,
      TabbarItem
  }
}

</script>
<style scoped>
</style>