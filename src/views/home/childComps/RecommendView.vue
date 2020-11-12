<template>
  <div class="recommend">
      <div v-for="(value,key) in recommend" :key="key" class="item">
          <a :href="value.link">
              <img :src="value.image" alt="" width="80rem">
              <div class="title">{{value.title}}</div>
          </a>
      </div>
  </div>
</template>

<script>
export default {
  props: {
    recommend: {
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
.recommend{
    display: flex;
    width: 100%;
    padding: 1rem 0;
    border-bottom: 0.8rem solid #eee;
}
.recommend>.item{
    flex: 1;
    text-align: center;
}
.recommend>.item .title{
    font-size: 0.8rem;
}
</style>