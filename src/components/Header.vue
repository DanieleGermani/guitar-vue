<script setup>
import Guitar from "./Guitar.vue";

const props = defineProps({
  cart: {
    type: Object,
    required: true,
  },
  guitar: {
    type: Object,
    required: true,
  },
});
defineEmits([
  "increase-quantity",
  "decrease-quantity",
  "remove-from-cart",
  "add-to-cart",
]);
</script>
<template>
  <header class="py-5 header">
    <div class="container-xl">
      <div class="row justify-content-center justify-content-md-between">
        <div class="col-8 col-md-3">
          <a href="index.html">
            <img class="img-fluid" src="/img/logo.svg" alt="imagen logo" />
          </a>
        </div>
        <nav
          class="col-md-6 a mt-5 d-flex align-items-start justify-content-end"
        >
          <div class="carrito">
            <img
              class="img-fluid"
              src="/img/carrito.png"
              alt="imagen carrito"
            />

            <div id="carrito" class="bg-white p-3">
              <p v-if="!cart.length" class="text-center m-0">
                El carrito esta vacio
              </p>
              <div v-else>
                <table class="w-100 table">
                  <thead>
                    <tr>
                      <th>Imagen</th>
                      <th>Nombre</th>
                      <th>Precio</th>
                      <th>Cantidad</th>
                      <th></th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="item in cart" :key="item.id">
                      <td>
                        <img
                          class="img-fluid"
                          :src="'img/' + item.image + '.jpg'"
                          :alt="'' + item.name + 'imagen guitarra'"
                        />
                      </td>
                      <td>{{ item.name }}</td>
                      <td class="fw-bold">${{ item.price }}</td>
                      <td class="flex align-items-start gap-4">
                        <button
                          @click="$emit('decrease-quantity', item)"
                          type="button"
                          class="btn btn-dark"
                        >
                          -
                        </button>
                        {{ item.quantity }}
                        <button
                          @click="$emit('increase-quantity', item)"
                          type="button"
                          class="btn btn-dark"
                        >
                          +
                        </button>
                      </td>
                      <td>
                        <button
                          @click="$emit('remove-from-cart', item)"
                          class="btn btn-danger"
                          type="button"
                        >
                          X
                        </button>
                      </td>
                    </tr>
                  </tbody>
                </table>

                <p class="text-end">
                  Total pagar: <span class="fw-bold">$899</span>
                </p>
                <button class="btn btn-dark w-100 mt-3 p-2">
                  Vaciar Carrito
                </button>
              </div>
            </div>
          </div>
        </nav>
      </div>
      <!--.row-->

      <div class="row mt-5">
        <div class="col-md-6 text-center text-md-start pt-5">
          <h1 class="display-2 fw-bold">Modelo {{ guitar.name }}</h1>
          <p class="mt-5 fs-5 text-white">
            {{ guitar.description }}
          </p>
          <p class="text-primary fs-1 fw-black">${{ guitar.price }}</p>
          <button
            type="button"
            class="btn fs-4 bg-primary text-white py-2 px-5"
            @click="$emit('add-to-cart', guitar)"
          >
            Agregar al Carrito
          </button>
        </div>
      </div>
    </div>

    <img
      class="header-guitarra"
      src="/img/header_guitarra.png"
      alt="imagen header"
    />
  </header>
</template>
