<script setup>
import {ref, computed} from 'vue'

const name = 'Vue dinamico';
const styleColor = "color: blue"; 
const arrayColores = ["blue", "red", "peru"]
const activo = false

const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"];

const arrayFrutas1 = [
    {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",
        id: 1,
    },
    {
        name: "Pera",
        price: "$2.00",
        description: "Una pera",
        id: 2,
    },
    {
        name: "Naranja",
        price: "$3.00",
        description: "Una naranja",
        id: 3,
    },
];

const objetoFruta = {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",
        id: 1,
}

const arrayFrutas3 = [
    {
        name: "Manzana",
        price: "$1.00",
        description: "Una manzana",
        stock: 0,
    },
    {
        name: "Pera",
        price: "$2.00",
        description: "Una pera",
        stock: 10,
    },
    {
        name: "Naranja",
        price: "$3.00",
        description: "Una naranja",
        stock: 20,
    },
];

//metodo - methods
const handleClick = (mensaje) => {
  console.log(mensaje)
}

const counter = ref(0)

const increment = () => {
  counter.value ++;
}

const decrement = () => {
  counter.value--;
}

const reset = () => {
  counter.value = 0
}

const classCounter = computed(() => {
  if(counter.value === 0){
    return 'cero'
  }
  if(counter.value > 0){
    return 'positivo'
  }
  if(counter.value < 0){
    return 'negativo'
  }
})

// Practica

const numeros = ref([])

const add = () => {
  numeros.value.push(counter.value)
}

const bloquearBtn = computed(() => {
  if (numeros.value.includes(counter.value)) {
    return true
  }else{
    return false
  }
})

</script>

<!-- Para conectar script con template a traves de v-bind o : con atributos -->
<!-- Con texto es mediante doble llave {{}} -->

<!-- Se pueden usar expresiones de JS -->
<!-- Acepta lo que tenga un retorno inmediato -->

<template>
    <h1>Hola {{ name.toUpperCase() }}</h1>
    <h2>{{ arrayColores }}</h2>
    <h2 :style="`color: ${arrayColores[2]}`">Soy Peru</h2>
    <h2>
        {{ activo ? "Estoy activo" : "Estoy inactivo" }}
    </h2>

    <br></br>

    <!-- v-if -->

    <h2 v-if="activo === true">
        <span>Icono</span>
        Estoy activo
    </h2>

    <p v-else-if="activo === false">Estoy inactivo</p>

    <p v-else>Estoy indeciso</p>

    <!-- v-show -->

    <h2 v-show="activo">Estoy activo v-show</h2>

    <br></br>

    <!-- v-for -->

    <ul>
        <li v-for="(fruta, index) in arrayFrutas" :key="index">
          {{index}} - {{fruta}}
        </li>
    </ul>

    <br></br>

    <ul>
        <li v-for="(fruta, index) in arrayFrutas1" :key="fruta.id">
            {{ fruta.name }} - {{ fruta.price }} - {{ fruta.description }}
        </li>
    </ul>

    <br></br>

    <ul>
        <li v-for="(value, propiedad, index) in objetoFruta" :key="index">
            {{ index }} - {{ propiedad }}: {{ value }}
        </li>
    </ul>

    <br></br>

    <!-- v-for + v-if -->

    <ul>
          <template v-for="item in arrayFrutas3" :key="item.name">
              <li v-if="item.stock > 0">
                  {{ item.name }} - {{ item.price }}
              </li>
          </template>
    </ul>

    <br></br>

    <!-- Eventos -->

    <button v-on:click.right.prevent="handleClick('Texto Right')">Activame right</button>
    <button @click.middle.prevent="handleClick('Texto Middle')">Activame middle</button>
    <button @click="handleClick('Texto Left')">Activame left</button>

    <br></br>
    <br></br>
    

    <!-- Reactividad -->

    <h2 :class="classCounter">{{ counter }}</h2>
    <button @click="increment">Aumentar</button>
    <button @click="decrement">Disminuir</button>
    <button @click="reset">Reset</button>
   
     <!-- Practica -->

     <button :disabled="bloquearBtn" @click="add">Add</button>
     <br></br>
     {{ numeros }}


    


</template>

<style>

h1{
  color:red
}

.positivo {
  color: lime
}

.negativo {
  color: red
}

.cero {
  color: orange
}


</style>
