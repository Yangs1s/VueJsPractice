<!-- @format -->

<template>
  <div v-if="1 == 1" class="banner">
    <h2>지금 결제하면 20% 할인</h2>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Discount",
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.banner {
  background: #eaeaea;
  padding: 10px;
  margin: 10px;
  border-radius: 20px;
}
</style>
