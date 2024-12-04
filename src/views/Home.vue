<template>
  <div class="home">
    <section class="hero is-medium mb-6">
        <div class="hero-body has-text-centered">
            <p class="title mb-6">
                Welcome to Priceless Empire 
            </p>
            <p class="subtitle">
                Experience the difference
            </p>
        </div>
    </section>

      <div class="container-fluid bg-trasparent my-4 p-3" style="position: relative">
      <div class="row row-cols-1 row-cols-xs-2 row-cols-sm-2 row-cols-lg-4 g-3">

      <div class="column is-12">
          <h2 class="is-size-2 has-text-centered">Latest products</h2>
      </div>

      <ProductBox 
        v-for="product in latestProducts"
        v-bind:key="product.id"
        v-bind:product="product" />
      </div>
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

    document.title = 'Home | Priceless'
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
<style lang='css' scoped>
  @import url('https://fonts.googleapis.com/css2?family=Tangerine:wght@700&display=swap');

  .hero-body {
    background: linear-gradient(90deg, #fcff9e 0%, #c67700 100%);
    border-radius: 10px;
    box-shadow: 0 2px 10px rgba(78, 35, 0, 0.418);
  }

  .subtitle{
    font-family: 'Tangerine', cursive;
    font-size: 30px;
  }

  .title{
    font-family: 'Tangerine', cursive;
    font-weight: bolder;
    font-size: 4rem;
  }
</style>