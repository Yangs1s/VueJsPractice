<!-- @format -->

<template>
  <div class="black-bg" v-if="modalIsOpen == true">
    <div class="white-bg">
      <img :src="products[clicked].image" class="detail-img" />
      <h4 style="font-weight: bolder; font-size: x-large">
        {{ products[clicked].title }}
      </h4>
      <p>{{ products[clicked].content }}</p>
      <div class="input-bar">
        <input v-model="month" />
        <input type="range" min="1" max="24" v-model="month" />
      </div>
      <p class="price">
        {{ month }}개월 선택:{{
          (products[clicked].price * month).toLocaleString("ko")
        }}
        원
      </p>
      <button @click="$emit('modalClose')" class="closebtn">닫기</button>
    </div>
  </div>
</template>
<!-- e파라미터 === $event -->
<!-- @input="month = $event.target.value" => v-model = "month" -->
<!-- v-model은 input,textarea,select 여러가지 input들 전부 가능합니다 -->
<script>
export default {
  name: "ModalPage",
  data() {
    return {
      month: 1,
    };
  },
  /// data를 감시하려면 watch를 쓴다.
  watch: {
    month(a) {
      if (a > 25 || isNaN(a) === true) {
        alert("숫자만 입력하세요");
        this.month = 1;
      }
    },
  },
  props: {
    // dataname: type 이런식으로 써줘야합니다.
    products: Array,
    clicked: Number,
    modalIsOpen: Boolean,
  },
};
</script>

<style>
.detail-img {
  width: 400px;
}
.price {
  font-size: small;
  font-weight: 500;
}
.input-bar {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>
