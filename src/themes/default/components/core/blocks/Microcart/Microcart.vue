<template>
  <div class="microcart bg-white c-black" :class="{ active: isOpen }">
    <div class="row">
      <div class="col-md-12 end-xs">
        <i class="material-icons p15 close c-black" @click="closeMicrocart">close</i>
      </div>
    </div>
    <h2 v-if="items.length" class="c-black ml30">Shopping cart</h2>
    <h4 v-if="!items.length" class="c-black ml30">Your shopping cart is empty.</h4>
    <em v-if="!items.length" class="ml30" @click="closeMicrocart">Don't hesitate and <router-link to="/">browse our catalog</router-link> to find something beatufiul for You!</em>
    <ul class="products">
      <product v-for="product in items" :key="product.id" :product="product" />
    </ul>
    <div v-if="items.length" class="checkout bg-lightgray pt10">
      <h3 class="ml30 c-black">Shopping summary</h3>
      <div class="row pt15 pb20 pl30 pr55">
        <div class="col-xs c-black">
          Subtotal
        </div>
        <div class="col-xs align-right c-black">
          {{ subtotal | price }}
        </div>
      </div>
      <div class="row pt20 pb20 pl30 pr55">
        <div class="col-xs c-black">
          Shipping ({{ shipping.name }})
        </div>
        <div class="col-xs align-right c-black">
          {{ shipping.cost | price }}
        </div>
      </div>
      <div class="row pt20 pb20 pl30 pr55">
        <div class="col-xs c-black">
          Payment ({{ payment.name }})
        </div>
        <div class="col-xs align-right c-black" v-if='payment.cost > 0'>
          {{ payment.cost | price }}
        </div>
      </div>
      <div class="row pt20 pb20 pl30 pr55">
        <div class="col-xs weight-400 c-black">
          Total
        </div>
        <div class="col-xs align-right weight-400 h3 c-black">
          {{ total | price }}
        </div>
      </div>
      <div class="row pt20 pb20 pl30 pr55" v-if="!isCheckoutMode">
        <div class="col-xs align-right">
              <router-link class="no-underline" :to="{ name: 'checkout' }"><button class="checkout-button bg-black brdr-none c-white pb20 pt20 pl70 pr70" @click="closeMicrocart">CHECKOUT</button></router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { coreComponent } from 'lib/themes'
import Product from './Product'

export default {
  created () {
    console.log('CI  ' + this.cartItems)
  },
  components: {
    Product
  },
  mixins: [coreComponent('core/blocks/Microcart/Microcart')]
}
</script>

<style lang="scss" scoped>
@import "../../../../css/transitions.scss";

  .microcart {
      height: 100vh;
      width: 800px;
      top: 0;
      right: 0;
      max-width: 100%;
      position: fixed;
      z-index: 3;
      transform: translateX(100%);
      transition: transform 300ms $motion-main;
      overflow-y: auto;
      overflow-x: hidden;
  }
  .microcart.active {
      transform: translateX(0)
  }
  .close {
    cursor: pointer;
  }
  i {
    opacity: 0.6;
  }
  i:hover {
    opacity: 1;
  }
</style>
