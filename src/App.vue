<script setup>
import { ref, reactive, onMounted, watch } from "vue";
import { db } from "./data/guitar";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";
import Guitar from "./components/Guitar.vue";

const guitars = ref([]);
const cart = ref([]);
const guitar = ref({});

watch(
  cart,
  () => {
    saveInLocalStorege();
  },
  { deep: true }
);

onMounted(() => {
  guitar.value = db[3];
  guitars.value = db;
  const cartLocalStorage = localStorage.getItem("cart");
  if (cartLocalStorage) {
    cart.value = JSON.parse(cartLocalStorage);
  }
});

const saveInLocalStorege = () => {
  localStorage.setItem("cart", JSON.stringify(cart.value));
};
const addToCart = (guitar) => {
  const guitarIndex = cart.value.findIndex((item) => item.id === guitar.id);
  if (guitarIndex >= 0) {
    cart.value[guitarIndex].quantity++;
  } else {
    guitar.quantity = 1;
    cart.value.push(guitar);
  }
};

const increaseQuantity = (guitar) => {
  guitar.quantity++;
};

const decreaseQuantity = (guitar) => {
  if (guitar.quantity <= 1) return;
  guitar.quantity--;
};

const removeGuitarFromCart = (guitar) => {
  const index = cart.value.findIndex((item) => item.id === guitar.id);
  if (index >= 0) {
    cart.value.splice(index, 1);
  }
};

const removeAllItem = () => {
  cart.value = [];
};
</script>

<template>
  <Header
    :cart="cart"
    :guitar="guitar"
    @increase-quantity="increaseQuantity"
    @decrease-quantity="decreaseQuantity"
    @remove-from-cart="removeGuitarFromCart"
    @add-to-cart="addToCart"
    @remove-all-items="removeAllItem"
  />
  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>

    <div class="row mt-5">
      <Guitar
        v-for="guitar in guitars"
        :key="guitar.id"
        v-bind:guitar="guitar"
        @add-to-cart="addToCart"
      />
    </div>
  </main>

  <Footer />
</template>

<style></style>
