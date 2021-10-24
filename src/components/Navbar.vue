<template>
  <div>
    <nav>
      <div class="container">
        <ul class="navbar-left">
          <li>
            <a href="#about" class="active">PRODUCTS</a>
          </li>
        </ul>
        <!--end navbar-left -->

        <ul class="navbar-right">
          <li>
            <a @click="toogleCart" href="#" id="cart"
              ><i class="fa fa-shopping-cart"></i> Cart <span class="badge">{{ basket.length }}</span></a
            >
          </li>
        </ul>
        <!--end navbar-right -->
      </div>
      <!--end container -->
    </nav>

    <div v-if="shoppingCardStatus && basket.length > 0" class="container">
      <div class="shopping-cart">
        <div class="shopping-cart-header">
          <i class="fa fa-shopping-cart cart-icon"></i><span class="badge">{{ basket.length }}</span>
          <div class="shopping-cart-total">
            <span class="lighter-text">Total:</span>
            <span class="main-color-text">${{ totalPrice() }}</span>
          </div>
        </div>
        <!--end shopping-cart-header -->

        <ul class="shopping-cart-items">
          <li class="clearfix" v-for="(items, i) in basket" :key="i">
            <img :src="require(`../assets/${items.src}`)" alt="" />
            <span class="item-name">{{ items.title }}</span>
            <span class="item-price">${{ items.price * (items.count + items.quantity - 1) }}</span>

            <div class="quantity">
              <span class="close-btn" type="button" @click="deleteProdcut(i)"><i class="fa fa-trash fa-lg" style="color:red" aria-hidden="true"></i></span>
              <button class="btn minus-btn  dec" @click="items.count == 0 ? 0 : items.count--" type="button">-</button>
              <input type="text" id="quantity" :value="items.count + items.quantity - 1" />
              <button class="btn plus-btn inc" @click="items.count++">+</button>
            </div>
          </li>
        </ul>
        <a href="#" class="button">Checkout</a>
      </div>
      <!--end shopping-cart -->
    </div>
  </div>
  <!--end container -->
</template>

<script>
export default {
  name: 'Navbar',
  props: {
    basket: Array,
    totalPrice: Function,
  },

  data() {
    return {
      shoppingCardStatus: false,
    };
  },

  methods: {
    // sepetin açılma ve kapanma durumları
    toogleCart() {
      this.shoppingCardStatus = !this.shoppingCardStatus;
    },
    // sepetten ürnü silme işlemi
    deleteProdcut(item) {
      this.basket.splice(item, 1);
    },
  },
  // Ürün sepete eklendiğinde alerti göster
};
</script>

<style scoped>
*,
*:before,
*:after {
  box-sizing: border-box;
}

body {
  font: 14px/22px 'Lato', Arial, sans-serif;
  background: #6394f8;
}

.lighter-text {
  color: #abb0be;
}

.main-color-text {
  color: #6394f8;
}

nav {
  padding: 20px 0 40px 0;
  background: #dabad2;
  font-size: 16px;
}
nav .navbar-left {
  float: left;
}
nav .navbar-right {
  float: right;
}

nav ul li {
  display: inline;
  padding-left: 20px;
}

nav ul li a {
  color: #777777;
  text-decoration: none;
}
nav ul li a:hover {
  color: black;
  text-decoration: none;
}
.container {
  margin: auto;
  width: 80%;
}

.badge {
  background-color: #6394f8;
  border-radius: 10px;
  color: white;
  display: inline-block;
  font-size: 12px;
  line-height: 1;
  padding: 3px 7px;
  text-align: center;
  vertical-align: middle;
  white-space: nowrap;
}

.shopping-cart {
  margin: 20px 0;
  float: right;
  margin-left: 53%;
  margin-top: -1px;
  background: #fff;
  width: 320px;
  position: absolute;
  border-radius: 3px;
  padding: 20px;
  z-index: 1;
}

.shopping-cart .shopping-cart-header {
  border-bottom: 1px solid #e8e8e8;
  padding-bottom: 15px;
}
.shopping-cart .shopping-cart-total {
  float: right;
}
.shopping-cart-items {
  padding-top: 20px;
}
.shopping-cart:after {
  bottom: 100%;
  left: 89%;
  border: solid transparent;
  content: ' ';
  height: 0;
  width: 0;
  position: absolute;
  pointer-events: none;
  border-bottom-color: white;
  border-width: 8px;
  margin-left: -8px;
}
.shopping-cart-items li {
  margin-bottom: 18px;
  list-style: none;
}

.shopping-cart-items img {
  float: left;
  margin-right: 12px;
  width: 90px;
  height: 80px;
}

.item-name {
  display: block;
  padding-top: 10px;
  font-size: 16px;
}

.item-price {
  color: #6394f8;
  margin-right: 8px;
}
.item-quantity {
  color: #abb0be;
}
.shopping-cart:after {
  bottom: 100%;
  left: 89%;
  border: solid transparent;
  content: ' ';
  height: 0;
  width: 0;
  position: absolute;
  pointer-events: none;
  border-bottom-color: white;
  border-width: 8px;
  margin-left: -8px;
}

.cart-icon {
  color: #515783;
  font-size: 24px;
  margin-right: 7px;
  float: left;
}

.button {
  background: #6394f8;
  color: white;
  text-align: center;
  padding: 12px;
  text-decoration: none;
  display: block;
  border-radius: 3px;
  font-size: 16px;
  margin: 25px 0 15px 0;
}
.button:hover {
  background: lighten(#6394f8, 3%);
}

.clearfix:after {
  content: '';
  display: table;
  clear: both;
}
.close-btn {
  font-size: 20px;
  font-weight: bold;
  color: #000;
}

.quantity {
  display: flex;
  justify-content: start;
  margin-top: 5px;
}
.quantity button {
  width: 25px;
  height: 30px;
  padding-top: 4px;
  padding-left: 7px;
  padding-bottom: 17px;
  border: 1px solid #000;
  font-size: 17px;
  border-radius: 0;
  background: #fff;
  margin-left: 9px;
}
.dec {
  color: red;
}
.inc {
  color: blue;
}
.quantity input {
  border: none;
  border-top: 1px solid #000;
  border-bottom: 1px solid #000;
  text-align: center;
  width: 20px;
  font-size: 17px;
  font-weight: 300px;
  margin-right: -9px;
}
</style>
