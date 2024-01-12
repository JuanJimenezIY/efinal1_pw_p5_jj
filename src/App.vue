<template>
  <div v-if="intento <5 " class="container">
    <div class="puntuacion">
      <p>Puntaje: {{ puntaje }}</p>
      <p>Intentos: {{ intento }}</p>
    </div>

    <div class="imagen">
      <ImagenComponente :nombrePokemon="nombre1" :imagenUrl="imagen1" />
      <ImagenComponente :nombrePokemon="nombre2" :imagenUrl="imagen2" />
      <ImagenComponente :nombrePokemon="nombre3" :imagenUrl="imagen3" />
    </div>

    <button @click="comenzarJuego()">Jugar</button>
  </div>
  <div v-if="intento > 4 && puntaje<10" class="intentos">
    <p>Has utilizado tus 5 intentos</p>
    <p>El juego ha terminado</p>
    <button @click="reiniciarJuego()">Nuevo Juego</button>
  </div>
  <div v-if="puntaje > 9" class="premio">
    <p>Puntaje: {{ puntaje }}</p>
    <p>Felicitaciones has ganado un premio de $10.000</p>
    <button @click="reiniciarJuego()">Nuevo Juego</button>
  </div>
</template>

<script>
import ImagenComponente from "./components/ImagenComponente.vue";

export default {
  name: "App",
  components: {
    ImagenComponente,
  },
  data() {
    return {
      puntaje: 0,
      intento: 0,

      nombre1: "XXXXXX",
      nombre2: "XXXXXX",
      nombre3: "XXXXXX",
      imagen1:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg",
      imagen2:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg",
      imagen3:
        "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg",
    };
  },
  methods: {
    async consumirAPI() {
      const { image, answer } = await fetch("https://yesno.wtf/api").then(
        (datos) => datos.json()
      );
      return {image, answer};
    },
    async comenzarJuego() {
      this.intento++;
      const resultado1 = await this.consumirAPI();
      this.imagen1 = resultado1.image;
      this.nombre1 = resultado1.answer;

     
      const resultado2 = await this.consumirAPI();
      this.imagen2 = resultado2.image;
      this.nombre2 = resultado2.answer;

   
      const resultado3 = await this.consumirAPI();
      this.imagen3 = resultado3.image;
      this.nombre3 = resultado3.answer;

      if(resultado1.answer==="yes" && resultado2.answer==="yes" && resultado3.answer==="yes"){
        this.puntaje+=5;
      }
      else if(resultado1.answer==='yes' && resultado2.answer=='yes'){
        this.puntaje+=2;
      }
          else if(resultado2.answer==='yes' && resultado3.answer=='yes'){
        this.puntaje+=2;
      }
       else if(resultado1.answer==='yes' && resultado3.answer=='yes'){
        this.puntaje+=2;
      }
      else if(resultado1.answer==="yes" ||resultado2.answer==='yes' ||resultado3.answer==='yes' ){
         this.puntaje+=1;
      }

    },
    reiniciarJuego() {
      (this.puntaje = 0),
        (this.intento = 0),
        (this.nombre1 = "XXXXXX"),
        (this.nombre2 = "XXXXXX"),
        (this.nombre3 = "XXXXXX"),
        (this.imagen1 =
          "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg"),
        (this.imagen2 =
          "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg"),
        (this.imagen3 =
          "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg");
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  display: block;
  justify-content: center;

  font-family: Arial, Helvetica, sans-serif;
  font-size: 20px;
}
.intentos {
  color: red;
  margin: 50px;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 20px;
  

}
.premio {
  color: blue;
    margin: 50px;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 20px;
}
.imagen {
  display: flex;

  align-content: center;
  justify-content: center;
}
img {
  height: 400px;
  widows: 400px;
}
.puntuacion {
  display: flex;
  align-content: center;
  justify-content: center;
}
p {
  margin: 0px 30px;
}
button {
  width: 50px;
}
</style>
