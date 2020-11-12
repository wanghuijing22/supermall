<template>
  <div class="tab-control">
    <div v-for="(value, key) in tabcontrol" :key="key" class="tab-control-item" :class="{ 'active': key==index }" @click="select(key)">
      <span>{{ value }}</span>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    tabcontrol: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
        index:0
    };
  },
  methods: {
      select(key){
          this.index=key
          this.$emit('tabindex',this.index)
      }
  }
};
</script>
<style scoped>
.tab-control{
    display: flex;
    text-align: center;
    font-size: 0.9rem;
    height: 40px;
    line-height: 40px;
    /* position: sticky;
    top: 44px; */
    background-color: #FFF;
    z-index: 999;
}
.tab-control-item{
    flex: 1;
}
.tab-control-item span{
    padding: 6px;
}
.tab-control .active{
    color: var(--color-high-text);
}
.tab-control .active span{
    border-bottom: 2px solid var(--color-tint);
}
</style>