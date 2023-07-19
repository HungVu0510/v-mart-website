<template>
  <div>
    <HomeCarousel :sale_items="sale_items" />
    <br/><br/>
    <v-container>
      <h1 class="text-md-h4 text-h6">Our Categories</h1>
      <br/>
      <CategorySlider :categories="categories"/>
      <br/><br/><br/>
      <Newsletter/>
    </v-container>
  </div>
</template>

<script>
import ScrollTop from '../components/ScrollTop.vue';
export default {
  components: { ScrollTop },
  async created() {
    this.sale_items = await this.$content("products")
      .where({ onSale: true })
      .fetch();
      this.products = await this.$axios.$get('http://localhost:3001/products')
      this.categories = await this.$axios.$get('http://localhost:3001/categories')
  },
  data() {
    return {
      products: null,
      sale_items: null,
      categories: null,
    };
  },
};
</script>

<style>

</style>