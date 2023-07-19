<template>
  <div>
    <Nav/>
    <v-container v-if="product">
        <v-row justify="center">
            <v-btn 
                color="primary"
                nuxt to="/products"
            >
                <v-icon size="20" class="mr-2">mdi-keyboard-backspace</v-icon>
                Back To Product Page
            </v-btn>
            <v-col cols="11" md="7">
                <h2 class="text-center text-md-h4 font-weight-bold">
                    {{ product.name }}
                </h2>
                <div class="text-center mt-2">
                    <v-rating 
                        readonly 
                        half-increments 
                        class="mb-2" 
                        color="yellow draken-2"
                        background-color="grey lighten-1" 
                        :value="product.ratings" 
                        dense 
                        size="20"
                    ></v-rating>
                    <v-chip
                          x-small
                          label
                          outlined
                          class="mr-1"
                          v-for="(t, i) in product.tags"
                          :key="`prod${product.id}-${i}`"
                        >
                          {{ t }}
                        </v-chip>
                </div>
                <br/>
                <v-img 
                    width="100%"
                    class="el rounded-lg"
                    height="50vh"
                    :src="product.image"
                ></v-img>
                <v-card-subtitle class="primary--text pb-3 text-md-h5 pl-0">
                    Product Price : {{ $formatMoney(product.price) }}
                </v-card-subtitle>
                <v-card-subtitle class="primary--text pb-3 text-md-h6 pl-0 py-0">
                    Onsale Price : {{ $formatMoney(product.salePrice) }}
                </v-card-subtitle>
                <v-card-subtitle class="primary--text pb-3 text-md-h6 pl-0 py-0 pb-0">
                    Produt Description:
                </v-card-subtitle>
                <p class="mb-7">
                    {{ product.description }}
                </p>
                <v-btn 
                    @click="$store.commit('cart/AddToCart', product)"
                    min-height="45" 
                    min-width="170" 
                    class="text-capitalize" 
                    color="primary"
                >
                Add To Cart
                </v-btn>
            </v-col>
        </v-row>
    </v-container>
    <br /><br />
    <Footer />
    <ScrollTop />
  </div>
</template>

<script>
export default {
    async created() {
      const p = await this.$axios.$get(`http://localhost:3001/products/${this.$route.params.id}`)
    //   .where({id: parseInt(this.$route.params.id)})
    //   .limit(1)
    //   .fetch();
      this.product = p;
    },
    data() {
        return {
            product: null,
        }
    }
}
</script>

<style>

</style>