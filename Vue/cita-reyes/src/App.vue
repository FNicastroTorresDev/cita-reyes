<script setup>
  import { computed, ref } from "vue"
  import { productos } from "./datos.js"
  import imagen1 from "./assets/oferta.jpg"

  const contador = ref(0)
  const total = productos.length

  const siguiente = () => {
    contador.value === total-1 ? contador.value = 0 : contador.value++
  } 

  const nombreRey = computed(()=>{
    const cadena = productos[contador.value].nombre
    return cadena.charAt(0).toUpperCase() + cadena.slice(1).toLowerCase() 
  })

  const imagenRey = computed(()=>{
    return `https://www.html6.es/img/rey_${productos[contador.value].nombre.toLowerCase()}.png`
  })

  const precioDescuento = computed( () => {
    return productos[contador.value].precio*0.9
  })
</script>

<template>
  <div class="container">
    <h1>Cena {{ contador+1 }} con rey godo <span class="green">{{ nombreRey }}</span></h1>
    <h3>Precio: <span class="green">${{ productos[contador].precio }}</span></h3>
    <span v-if="productos[contador].finDeSemana" class="green-medalla">(De lunes a domingo)</span>
    <span v-else class="red-medalla">(Solo fines de semana)</span>
    <span v-if="productos[contador].precio<100" class="descuento">
      Ahora con 10% de dto: <span class="green"> ${{ precioDescuento }}</span>
      <img v-bind:src="imagen1" class="oferta" alt="banner de Oferta"/>
    </span>
    <img :src="imagenRey" class="fotoRey" alt="Foto Rey" />
    <button v-on:click="siguiente">Siguiente ({{ contador+1 }}/{{ total }})</button>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  font-family: Helvetica, Arial, sans-serif;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 32px;
}
h1 {
  font-size: 1.5rem;
  margin: 0 0 24px;
  text-align: center;
}
.green {
  font-size: 1.6rem;
  color: green;
}
.green-medalla {
  padding: 3px 8px;
  border-radius: 2px;
  background-color: green;
  color: white;
  margin: 8px 0;
}
.red-medalla {
  padding: 3px 8px;
  border-radius: 2px;
  background-color: red;
  color: white;
  margin: 8px 0;
}
.descuento {
  display: flex;
  align-items: center;
}
.oferta {
  height: 24px;
  width: auto;
}
.fotoRey {
  margin: 32px 0;
}
button {
  padding: 4px 6px;
}
</style>
