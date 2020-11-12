<!--  -->
<template>
  <div class="tabbar-item" @click="itemClick">
      <!-- 在插槽外面套一层div是为了避免插槽标签出错 当panduan为true时高亮显示 -->
      <div v-if="!panduan"><slot name="tabbarImg"></slot></div>
      <!-- 高亮显示 -->
      <div v-else><slot name="tabbarImg-light"></slot></div>
      <!-- 当panduan为true时添加light的类 -->
      <div :style="lightColor"><slot name="tabbarText"></slot></div>
  </div>
</template>

<script>
export default {
  props:{
    path: String,
    itemColor:{//将item颜色改成动态的
      type:String,
      default:'#E7637A'//设置当不修改itemColor时默认值
    }
  },
  data () {
    return {
    };
  },
  computed: {//计算属性
    panduan(){//set不写就是函数
      return this.$route.path.indexOf(this.path) !== -1
    },
    lightColor(){//内容太过复杂可以将动态修改的内容放到computed中
      return this.panduan?{color:this.itemColor}:{}
    }
  },
  methods: {
    itemClick(){
      // console.log(this.path);
      this.$router.push(this.path)
    },
    
  },
}

</script>
<style scoped>

.tabbar-item {
  height: 49px;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.tabbar-item img{
    margin: 0;
    padding: 0;
    vertical-align: middle;
    width: 25px;
    height: 25px;
}
.tabbar-item div{
    font-size: 12px;
}
</style>