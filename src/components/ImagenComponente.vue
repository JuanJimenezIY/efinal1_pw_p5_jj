<template>
  <div class="container">
  
    <img v-bind:src="imagenUrl" alt="No se encuentra la imagen">

     <p > {{nombrePokemon}}</p>
  </div>
</template>

<script>
export default {

 props: {
        imagenUrl: {
            type: String,
            required: true
        },
        nombrePokemon: {
            type: String,
            required: true

        }
        },
data(){
   
}
}
</script>

<style scoped>

.container{
  display: grid;
  margin: 20px;
}
</style>>