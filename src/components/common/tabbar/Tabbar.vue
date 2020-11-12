<template>
  <div>
    <div id="tabbar">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
};
</script>
<style scoped>
#tabbar {
  display: flex;
  justify-content: space-around;
  background-color: #f6f6f6;
  position: fixed;
  right: 0;
  left: 0;
  bottom: 0;
  box-shadow: 0 0 3px rgb(190, 190, 190);
}

</style>