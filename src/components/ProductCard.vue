<template>
  <div class="container w-50 ">
    <div class="card shadow-lg col-md-8">
      <div class="mt-3">
        <div class="procut-1 align-items-center p-2 text-center">
          <img :src="require(`../assets/${info.src}`)" class="img-fluid img" width="360" alt="img" />
          <h5>{{ info.title }}</h5>

          <!-- card info -->
          <div class="mt-3 info">
            <span class="text1 d-block">{{ info.description }}</span>
          </div>
          <div class="cost mt-3 text-dark">
            <span>${{ this.priceSizeCost == 0 ? 150 : this.priceSizeCost }}</span>
            <p class="chose">choose size</p>
            <div class="size mt-3 align-items-center ">
              <button @click="priceSizeTotal(size)" v-for="(size, i) in info.size" :key="i" :class="{ sizeBtnBlue: info.color == 'blue', sizeBtnPink: info.color == 'pink' }" class="btn btn-outline  mx-1">{{ size }}</button>
            </div>
            <div class="d-flex justify-content-center align-items-center ml-auto mt-3">
              <div class="star col-md-6 ">
                <button @click="(info.src = 'blue-shoe.jpg'), (info.color = 'blue')" class="btn btn-primary mx-1 color"></button>
                <button @click="(info.src = 'pink-shoe.jpg'), (info.color = 'pink')" class="btn btn-danger mx-1 color"></button>
              </div>

              <div class="quantity">
                <span class="">Quantity:</span>
                <button class="btn minus-btn  dec" @click="info.quantity == 1 ? 1 : info.quantity--" type="button">-</button>
                <input type="text" id="quantity" :value="info.quantity" />
                <button class="btn plus-btn inc" @click="info.quantity++">+</button>
              </div>
            </div>

            <div class=" mt-3  align-items-center">
              <i v-for="(rating, i) in info.rating" :key="i" class="fa fa-star star"></i>
              <span v-if="info.rating < 5"> <i v-for="(data, i) in 5 - info.rating" :key="i" class="fa fa-star notChecked"></i> </span>
            </div>
          </div>
        </div>

        <!-- button for cards -->
        <div type="button" :class="{ blue: info.color == 'blue', pink: info.color == 'pink' }" @click="addToBasket(info)" class="p-3 shoe text-center text-white mt-3 ">
          <span class="text-uppercase ">Add to cart</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
    info: Object,
    basket: Array,
  },
  data() {
    return {
      priceSizeCost: 0,
      sizeVal: 0,
      attachedClass: 'danger',
    };
  },

  methods: {
    // emit ile parent componente
    addToBasket(val) {
      this.$swal('Ürün sepete eklendi...'); // alert box
      val.price += this.sizeVal;
      //  val.price = this.priceSizeCost;

      this.$emit('addProduct', val);
    },
    // boy + fiyat = yeni fiyat
    priceSizeTotal(sizeVal) {
      this.sizeVal = sizeVal;
      this.priceSizeCost = sizeVal + this.info.price;
    },
  },
};
</script>

<style scoped>
.container {
  margin: 100px 0 100px 0;
  display: inline-flex;
  justify-content: space-evenly;
  align-items: center;
}

.card {
  border: none;
  outline: none;
  background-color: #fff;
  border-radius: 20px;
}
.card:hover {
  transform: translateY(-15px);
  transition: transform 0.3s;
}
.text1 {
  font-size: 16px;
}
.info {
  line-height: 17px;
}
.star {
  color: #fbc02d;
}
.notChecked {
  font-size: 16px;
}

.cost span {
  color: rgb(2, 2, 78);
  font-weight: bold;
  font-size: 20px;
}
p {
  font-size: 0.9em;
  color: #95afc0;
  letter-spacing: 1px;
}
.sizeBtnBlue {
  border: 2px solid rgb(1, 83, 110);
  font-size: 20px;
  color: rgb(1, 83, 110);
  transition: 1s;
}
.sizeBtnBlue:hover {
  background-color: rgb(1, 83, 110);
  color: #fff;
  transition: 1s;
}
.sizeBtnPink {
  border: 2px solid rgb(245, 160, 174);
  font-size: 20px;
  color: rgb(245, 160, 174);
  transition: 1s;
}
.sizeBtnPink:hover {
  background-color: rgb(245, 160, 174);
  color: #fff;
  transition: 1s;
}

.chose {
  margin-top: 11px;
  margin-bottom: 0;
  margin-left: 20px;
}

.pink {
  background: rgb(245, 160, 174);
}
.blue {
  background: rgb(1, 83, 110);
}
.shoe {
  border-radius: 0 0 20px 20px;
  cursor: pointer;
  transition: 1s;
}
.shoe:hover {
  opacity: 0.9;
  transition: 1s;
}
.color {
  border-radius: 50px;
}
.quantity {
  display: flex;
  justify-content: start;
  margin-right: 75px;
  margin-top: 5px;
}
.quantity button {
  width: 25px;
  height: 30px;
  padding: 4px 7px 30px 7px;
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
