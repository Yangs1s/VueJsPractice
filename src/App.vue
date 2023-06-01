<!-- @format -->

<template>
  <Discount />

  <button @click="increaseSort">오름차순 정렬</button>
  <button @click="decreaseSort">내림차순 정렬</button>
  <!-- transiton vue에서 제공하는 애니메이션 쉽게 줄수 있는 태그임 -->
  <Transition name="fade">
    <Modal
      :products="products"
      :clicked="clicked"
      :modalIsOpen="modalIsOpen"
      @modalClose="modalIsOpen = false"
    />
  </Transition>

  <div class="menu">
    <a v-for="tab in menuTabs" :key="tab">{{ tab }}</a>
  </div>

  <div class="product-list">
    <CardItem
      :product="product"
      @openModal="
        modalIsOpen = true;
        clicked = $event;
      "
      v-for="product in products"
      :key="product"
    />
  </div>
</template>

<script>
import products from "./data.js";
import Discount from "./components/Discount";
import Modal from "./Modal.vue";
import CardItem from "@/components/Card.vue";
export default {
  name: "App",
  data() {
    // data보관함
    return {
      clicked: 0,
      modalIsOpen: false,
      products: products,
      menuTabs: ["Home", "Shop", "About"],
    };
  },
  methods: {
    //함수 만들려면 여기다가
    increase() {
      console.log(this.products);
      this.products.map((item, i) => console.log(item, i));
    },
    increaseSort() {
      this.products.sort((a, b) => {
        // 오름차순
        if (a.price < b.price) {
          return -1;
        }
        if (a.price > b.price) {
          return 1;
        }

        return 0;
      });
    },
    decreaseSort() {
      this.products.sort((a, b) => {
        // 오름차순
        if (a.price > b.price) {
          return -1;
        }
        if (a.price < b.price) {
          return 1;
        }
        return 0;
      });
    },
  },
  components: {
    Discount,
    Modal,
    CardItem,
  },
};
</script>

<!-- 
  .fade-enter-from // 시작시
  .fade-enter-active // 움직이는 방법
  .fade-enter-to // 끝

  fade는 작명한거임 다른거 들어가도 됨
  반대의 행동할시 enter를 leave로 바꿔준다
 -->
<style>
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 0.6s;
}
.fade-leave-to {
  opacity: 0;
}

.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 0.6s;
}
.fade-enter-to {
  opacity: 1;
}
body {
  margin: 0;
}
div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  padding: 20px;
}
.white-bg {
  width: 40%;
  background: white;
  border-radius: 8px;
  padding: 20px;
  margin: auto;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}

.products {
  width: auto;
  cursor: pointer;
}
.product-list {
  width: 100%;
  gap: 20px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}
.products img {
  width: 500px;
  margin-top: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

<!-- vue는 부모가 보내준 데이터를 함부로 조작할수가 없다. 그래서 쓰는게 $emit()이다.  
$event는 자식컴퍼넌트가 보낸 아이디값
-->
