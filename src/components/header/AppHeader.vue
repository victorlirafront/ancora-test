<template>
  <header class="header">
    <div class="header__container">
      <div class="logo-icon">
        <router-link to="/">
          <img class="ancora-logo" :src="IMAGES.ANCORA_LOGO" alt="Ancora logo" />
        </router-link>
      </div>

      <div class="container-login">
        <div class="login">
          <p>
            <router-link to="/login"> Olá, Faça seu login</router-link>
          </p>
        </div>
        <div class="header__cart-wrapper" @click="toggleCheckout">
          <div class="header__cart" ref="cartText">
            <img class="header__cart-img" :src="IMAGES.LOGO" alt="cart icon" />
            <p class="quantity">{{ quantity }}</p>
          </div>
        </div>
      </div>

      <Checkout v-if="isCheckoutVisible" class="header__checkout" @closeCheckout="closeCheckout" />
    </div>
  </header>
</template>

<script lang="ts">
import { useCartStore } from '@/src/stores/cart'
import { computed } from 'vue'
import Checkout from '../checkout/AppCheckout.vue'
import { IMAGES } from '@/src/constants/images'

export default {
  name: 'AppHeader',
  components: {
    Checkout,
  },
  data() {
    return {
      isCheckoutVisible: false,
    }
  },
  setup() {
    const cart = useCartStore()
    const quantity = computed(() =>
      cart.cartItems.reduce((total, item) => total + item.quantity, 0),
    )

    return {
      quantity,
    }
  },
  computed: {
    IMAGES() {
      return IMAGES
    },
  },
  methods: {
    toggleCheckout() {
      this.isCheckoutVisible = !this.isCheckoutVisible
    },
    closeCheckout() {
      this.isCheckoutVisible = false
    },
  },
}
</script>

<style scoped lang="scss">
@use './header.scss' as *;
</style>