<script setup>
import {ref} from "vue";
const products = ref([
{
  id:1,
  name: 'Asus',
  date: '20.11.2024',
  count: 10,
  price: 1000,
},
{
  id:2,
  name: 'Acer',
  date: '10.11.2024',
  count: 150,
  price: 1000,
},
{
  id:3,
  name: 'HP',
  date: '02.11.2024',
  count: 180,
  price: 1000,
}
]);

const name = ref('');
const date = ref('');
const count = ref(1);
const price = ref(0);
const addProduct = () => {
  if (name.value && date.value && count.value && price.value) {
    products.value.push({
id: Date.now(),
name: name.value,
date: date.value,
count: count.value,
price: price.value,
    })
  }
}

const removeProduct = (id) => {
  products.value = products.value.filter((product) => product.id != id);
}

const totalSum = computed(() => {
 return products.value.reduce((sum, product) => sum + (product.price*product.count), 0);
});

</script>

<template>
<div class="container">
<div class="row">
    <div class="mb-3">
  <label for="name" class="form-label">Название </label>
  <input type="text" v-model="name" class="form-control " id="name">
</div>
<div class="mb-3">
  <label for="date" class="form-label">Дата</label>
  <input type="date" v-model="date" class="form-control" id="date">
</div>
<div class="mb-3">
  <label for="count" class="form-label">Количество</label>
  <input type="number" v-model="count" class="form-control" id="count">
</div>
<div class="mb-3">
  <label for="price" class="form-label">Цена</label>
  <input  type="number" v-model="price" class="form-control" id="price">
</div>
<div class="button"></div>
<button @click="addProduct" type="button" class="btn btn-success my-5">Success</button>
</div>

<div class="row row-cols-1 row-cols-md-2 g-4">
  <div class="col" v-for="product in products" :key="product.id">
    <div class="card H-100">
      <div class="card-body">
        <h5 class="card-title">{{ product.name }} </h5>
        <p class="card-text">${{ product.price }}</p>
        <p class="card-text">X{{ product.count }}</p>
        <p class="card-text">{{ product.date }}</p>
      </div>
<div class="card-footer text end"></div>
<button @click="removeProduct(product.id)" class="btn btn-outline-danger mx-4">Удалить</button>
    </div>
  </div>
</div>
<div class="row my-4">
<div class="col">
  <h3 class="text-end">Общая сумма товаров: ${{ totalSum }}</h3>
</div>
</div>

</div>

</template>

<style scoped>

</style>
