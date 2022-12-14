<script setup>
import { ref, computed } from 'vue';

const name = 'Vue Dinámico'
// const styleColor = "color:blue"
// const arrayColores = ["blue", "red", "peru"]
// const activo = false
// const arrayFrutas = [
//   {
//     name: "Manzana",
//     price: "$1.00",
//     description: "Una manzana",
//     stock: 0,
//   },
//   {
//     name: "Pera",
//     price: "$2.00",
//     description: "Una pera",
//     stock: 10,
//   },
//   {
//     name: "Naranja",
//     price: "$3.00",
//     description: "Una naranja",
//     stock: 20,
//   },
// ];

// const fruta = {
//   name: "Naranja",
//   price: "$3.00",
//   description: "Una naranja",
// };

// Método - methods
const counter = ref(0);
const arrayNumber = ref([]);

const increment = () => {
  counter.value++

};
const decrement = () => {
  counter.value--

};
const reset = () => {
  counter.value = 0;
  arrayNumber.value = [];
};


const agregarNumero = computed(() => {
  arrayNumber.value.push(counter.value)
})

const bloquearAgregarNumero = computed(() => {
  const numSearch = arrayNumber.value.find((num) => num === counter.value)

  return numSearch || numSearch === 0;
})

const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'cero'
  }
  if (counter.value > 0) {
    return 'positivo'
  }
  if (counter.value < 0) {
    return 'negative'
  }
})

</script>

<template>
  <div class="container text-center mt-3">
    <h1>{{ name.toUpperCase() }}</h1>

    <!-- <button v-on:click.right.prevent="handleClick('Texto Right')">Actívame right</button>
  <button @click="handleClick('Texto Left')">Actívame left</button>
  <button @click.middle="handleClick('Texto Middle')">Actívame middle</button> -->
    <!-- 
  <h2>======= V-FOR con array de Objetos =======</h2>
  <ul>
    <li v-for="(fruta) in arrayFrutas" :key="name">
      {{ fruta.name }} - {{ fruta.price }} - {{ fruta.description }}
    </li>
  </ul>

  <h2>============ V-FOR con Objetos ============</h2>
  {{ fruta }}
  <ul>
    <li v-for="(value, propiedad, index) in fruta" :key="index">
      {{ index }} - {{ propiedad }} : {{ value }}
    </li>
  </ul>

  <h2>============ V-FOR y V-IF juntos ===========</h2>
  <ul>
    <template v-for="item in arrayFrutas" :key="item.name">
      <li v-if="item.stock > 0">{{ item.name }} - {{ item.price }}</li>
    </template>
  </ul>
-->
    <h2 :class="classCounter">{{ counter }}</h2>
    <div class="btn-group">
      <button class="btn btn-success" :disabled="counter >= 10 ? true : false" @click="increment">Aumentar</button>
      <button class="btn btn-warning" @click="reset">Resetear</button>
      <button class="btn btn-danger" :disabled="counter <= 0 ? true : false" @click="decrement">Disminuir</button>

      <button class="btn btn-primary" :disabled="bloquearAgregarNumero" @click="agregarNumero">Agregar</button>
    </div>

    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(numero, index) in arrayNumber" :key="index">{{ numero }}</li>
    </ul>
  </div>

</template> 

<style>
h1 {
  color: darkgreen;
}

.positivo {
  color: green;
}

.negativo {
  color: red;
}

.cero {
  color: peru;
}

.deshabilitado {
  display: none;
}
</style>