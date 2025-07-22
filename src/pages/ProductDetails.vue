<template>
  <section>
    <h2>{{ title }}</h2>
    <h3>${{ price}}</h3>
    <p>{{ description}}</p>
    <!-- Since below is going to load in the same page data will not update so move
    all the data extracting logic to the computed property of the component -->
    <router-link to="/products/p2">Product 2</router-link>
  </section>
</template>

<script>
import {  inject, computed } from 'vue';
import { useRoute } from 'vue-router';

export default {
  props: ['pid'],
  setup() {
    const products = inject('products');
    const route = useRoute();

    console.log(route);

    //since accessing with router object so removing props
    
    // const selectedProduct = computed(() => products.value.find(product => product.id === props.pid));
    const selectedProduct = computed(() => products.value.find(product => product.id === route.params.pid));
    
    const title = computed(() =>selectedProduct.value.title); // or selectedProduct.value['title']
    const price = computed(() =>selectedProduct.value.price); //as selectedProduct is a ref as returned from computed method so we need to use value property to access the value
    const description = computed(() =>selectedProduct.value.description);

    return { title, price, description };
  },
};
</script>


<style scoped>
section {
  margin: 3rem auto;
  max-width: 40rem;
  padding: 1rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
}
</style>