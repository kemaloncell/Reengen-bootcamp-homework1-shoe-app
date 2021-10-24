<template>
  <div id="app">
    <Navbar :basket="basket" :totalPrice="totalPrice" />
    <ProductCard v-for="(items, i) in productList" :key="i" :info="items" @addProduct="addProduct" />
  </div>
</template>

<script>
import ProductCard from './components/ProductCard.vue';
import Navbar from './components/Navbar.vue';
export default {
  name: 'App',
  components: {
    ProductCard,
    Navbar,
  },
  data() {
    return {
      productList: [
        {
          title: 'Nike Epic React Flyknit Sky Blue',
          price: 150,
          description: 'Best for running and having fun in the nature ',
          size: [5, 6, 7, 8, 9, 10, 11],
          color: 'blue',
          quantity: 1,
          rating: 3,
          src: 'blue-shoe.jpg',
        },
        {
          title: 'Nike Epic React Flyknit Sky Pink',
          price: 150,
          description: 'Best for running and having fun in the nature ',
          size: [5, 6, 7, 8, 9, 10, 11],
          color: 'pink',
          quantity: 1,
          rating: 2,
          src: 'pink-shoe.jpg',
        },
        {
          title: 'Nike Epic React Flyknit Sky Blue',
          price: 150,
          description: 'Best for running and having fun in the nature ',
          size: [5, 6, 7, 8, 9, 10, 11],
          color: 'blue',
          quantity: 1,
          rating: 4,
          src: 'blue-shoe.jpg',
        },
        {
          title: 'Nike Epic React Flyknit Sky Pink',
          price: 150,
          description: 'Best for running and having fun in the nature ',
          size: [5, 6, 7, 8, 9, 10, 11],
          color: 'pink',
          quantity: 1,
          rating: 5,
          src: 'pink-shoe.jpg',
        },
      ],
      basket: [],
    };
  },

  // sepette ürünleri ekliyoruz aynı ürünlerin tekrar eklenmesini engelliyoruz
  methods: {
    addProduct(e) {
      let isSameItem = this.basket.filter((el) => el.title === e.title).length;
      if (isSameItem) {
        let index = this.basket.findIndex((el) => el.title === e.title);
        this.basket[index].count++;
      } else {
        this.basket.unshift({ ...e, count: 1 });
      }
    },
    // toplam ücret
    totalPrice() {
      if (this.basket.length > 0) {
        return this.basket.map((item) => item.price * (item.quantity - 1 + item.count)).reduce((a, b) => a + b);
      } else {
        return 0;
      }
    },
  },
};
</script>
