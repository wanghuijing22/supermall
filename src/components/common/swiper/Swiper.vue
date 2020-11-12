<template>
  <div id="hy-swiper">
    <div
      class="swiper"
      @touchstart="touchStart"
      @touchmove="touchMove"
      @touchend="touchEnd"
    >
      <slot></slot>
    </div>
    <slot name="indicator"></slot>
    <div class="indicator">
      <slot name="indicator" v-if="showIndicator && slideCount > 1">
        <div
          v-for="(item, index) in slideCount"
          class="indi-item"
          :class="{ active: index === currentIndex - 1 }"
          :key="index"
        ></div>
      </slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    interval: {
      type: Number,
      default: 3000,
    },
    animDuration: {
      type: Number,
      defaule: 300,
    },
    moveRation: {
      type: Number,
      defaule: 0.25,
    },
    showIndicator: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      slideCount: 0, //元素个数
      totalWidth: 0, //swiper的宽度
      swiperStyle: {}, //swiper样式
      currentIndex: 1, //当前的index
      scrolling: false, //是否正在滚动
    };
  },
  mounted() {
    //操作DOM，在前后添加Slide
    setTimeout(() => {
      this.handleDom();
      //开启定时器
      this.startTimer();
    }, 100);
  },
  methods: {
    //   定时操作
    startTimer() {
      this.playTimer = window.setInterval(() => {
        this.currentIndex++,
          this.scrollContent(-this.currentIndex * this.totalWidth);
      }, this.interval);
    },
    stopTimer() {
      window.clearInterval(this.playTimer);
    },
    // 滚动到正确位置
    scrollContent(currentPosition) {
      //设置正在滚动
      this.scrolling = true;
      //开始滚动动画
      this.swiperStyle.transition = "transfrom" + this.animDuration + "ms";
      this.setTransform(currentPosition);
      //判断滚动到的位置
      this.checkPosition();
      //滚动完成
      this.scrolling = false;
    },
    // 校验正确位置
    checkPosition() {
      setTimeout(() => {
        this.swiperStyle.transition = "0ms";
        if (this.currentIndex >= this.slideCount + 1) {
          this.currentIndex = 1;
          this.setTransform(-this.currentIndex * this.totalWidth);
        } else if (this.currentIndex <= 0) {
          this.currentIndex = this.slideCount;
          this.setTransform(-this.currentIndex * this.totalWidth);
        }
        //结束移动后回调
        this.$emit("transitionEnd", this.currentIndex - 1);
      }, this.animDuration);
    },
    // 设置滚动位置
    setTransform(position) {
      this.swiperStyle.transform = `translate3d(${position}px ,0,0)`;
      this.swiperStyle[`-webkit-transform`] = `tramslate3d(${position}px,0,0)`;
      this.swiperStyle[`-ms-transform`] = `tramslate3d(${position}px,0,0)`;
    },
    // 操作DOM，在DOM前后添加Slide
    handleDom() {
      // 获取操作元素
      let swiperEl = document.querySelector(".swiper");
      let slidesEls = swiperEl.getElementsByClassName("slide");
      // 保存个数
      this.slideCount = slidesEls.length;
      //如果大于1就在前后分别添加slide
      if (this.slideCount > 1) {
        let cloneFirst = slidesEls[0].cloneNode(true);
        let cloneLast = slidesEls[this.slideCount - 1].cloneNode(true);
        swiperEl.insertBefore(cloneLast, slidesEls[0]);
        swiperEl.appendChild(cloneFirst);
        this.totalWidth = swiperEl.offsetWidth;
        this.swiperStyle = swiperEl.style;
      }
      //让swiper元素，显示第一个（目前显示前面添加的最后一个元素）
      this.setTransform(-this.totalWidth);
    },
    // 拖动事件处理
    touchStart: function (e) {
      //如果正在滚动 不可以拖动
      if (this.scrolling) return;
      //停止定时器
      this.stopTimer();
      //保存开始滚动位置
      this.startX = e.touches[0].pageX;
    },
    touchMove: function (e) {
      // 计算用户拖动的距离
      this.currentX = e.touches[0].pageX;
      this.distance = this.currentX - this.startX;
      let currentPosition = -this.currentIndex * this.totalWidth;
      let moveDistance = this.distance + currentPosition;
      //设置当前位置
      this.setTransform(moveDistance);
    },
    touchEnd: function (e) {
      //获取移动距离
      let currentMove = Math.abs(this.distance);
      //判断最终距离
      if (this.distance === 0) {
        return;
      } else if (
        this.distance > 0 &&
        currentMove > this.totalWidth * this.moveRation
      ) {
        //右边移动超过0.5
        this.currentIndex--;
      } else if (
        this.distance < 0 &&
        currentMove > this.totalWidth * this.moveRation
      ) {
        //向左移动超过0.5
        this.currentIndex++;
      }
      // 移动到正确位置
      this.scrollContent(-this.currentIndex - this.totalWidth);
      //移动完成后重新开始计时
      this.startTimer();
    },
    //控制上一个下一个
    previous() {
      this.changeItem(-1);
    },
    next() {
      this.changeItem(1);
    },
    changeItem(num) {
      //移除计时器
      this.stopTimer();
      //修改index和位置
      this.currentIndex += num;
      this.scrollContent(-this.currentIndex * this.totalWidth);
      //添加定时器
      this.startTimer();
    },
  },
};
</script>
<style scoped>
#hy-swiper {
  overflow: hidden;
  position: relative;
}
.swiper {
  display: flex;
}
.indicator {
  display: flex;
  justify-content: center;
  position: absolute;
  width: 10%;
  bottom: 8px;
  left: 50%;
}
.indi-item {
  box-sizing: border-box;
  width: 8px;
  height: 8px;
  border-radius: 4px;
  background-color: #000;
  line-height: 8px;
  text-align: center;
  font-size: 12px;
  margin: 0 5px;
}
.indi-item.active {
  background-color: rgba(212, 62, 46, 1);
}
</style>