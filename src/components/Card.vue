<!-- @format -->

<template>
  <div class="products" @click="clicked">
    <img v-bind:src="product.image" alt="home" />
    <h4>
      {{ product.title }}
    </h4>
    <p>월세 {{ product.price.toLocaleString("ko") }}</p>
  </div>
</template>
<!-- props로 받아오는 데이터는 수정이 안됩니다. -->
<script>
export default {
  name: "CardItem",
  props: {
    product: Object,
  },
  methods: {
    clicked() {
      this.$emit("openModal", this.product.id);
    },
  },
};
</script>

<style></style>
