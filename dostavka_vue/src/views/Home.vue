<template>
  <div class="home">
    <section class="hero is-dark is-medium mb-6">
      <div class="hero-body has-text-centered mt-1">
        <p class="title mb-6">
                Welcome to Taho &#5794; &#5800;
            </p>
            <p class="subtitle">
                The best store online
            </p>

      </div>
    </section>

    <div class="columns is-multiline">
      <div class="column is-12">
        <h2 class="is-size-2 has-text-centered">All you need is...</h2>
      </div>

      <ProductBox
        v-for="product in latestProducts"
        v-bind:key="product.id"
        v-bind:product="product" />

    </div>

  </div>
</template>

<script>
import axios from 'axios'

import ProductBox from '@/components/ProductBox'

export default {
  name: 'Home',
  data() {
    return {
      latestProducts: []
    }
  },
  components: {
    ProductBox
  },
  mounted() {
    this.getLatestProducts()
    document.title = 'Home | Taho'

  },
  methods: {
    async getLatestProducts() {

      this.$store.commit('setIsLoading', true)

      await axios
        .get('/api/v1/latest-products/')
        .then(response => {
          this.latestProducts = response.data
        })
        .catch(error => {
          console.log(error)
        })
      this.$store.commit('setIsLoading', false)

    }
  }
}
</script>