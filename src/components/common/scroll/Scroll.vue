<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  props: {
    probeType: {
      type: Number,
      default: 0,
    },
    pullUpLoad: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      scroll: null,
    };
  },
  mounted() {
    this.scroll = new BScroll(this.$refs.wrapper, {
      click: true,
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad,
    });
    //查看实时滚动的位置
    this.scroll.on("scroll", (position) => {
      this.$emit("scroll", position);
    });
    //下拉加载更多
    this.scroll.on("pullingUp",()=>{
        this.$emit('pullingUp')
    })
    console.log(this.scroll);
  },
  methods: {
    scrollTo(x, y, time = 400) {
      this.scroll.scrollTo(x, y, time);
    },
    finishPullUp(){
        this.scroll.finishPullUp();
    }
  },
};
</script>
<style scoped>
</style>