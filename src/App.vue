<template>
  <div class="container mt-4">
    <h1 class="text-center mt-5 mb-5">Listado de Canciones</h1>
    <div class="row mt-5">
      <div class="formu col-4">
        <form @submit.prevent="submit">
          <div class="mb-3">
            <label for="artista" class="form-label">Artista</label>
            <input class="form-control" type="text" v-model="artista"/>
            <div>
              <div v-if="artista.length === 0" class="card p-2 alert alert-warning">
                 <h6 class="text-center">Escribe nombre de artista</h6>
                </div>
              </div>
            <label for="cancion" class="form-label">Canción</label>
            <input class="form-control" type="text" v-model="cancion"/>
            <div>
            <div v-if="cancion.length === 0" class="card p-2 alert alert-warning">
      <h6 class="text-center">Escribe nombre de canción</h6>
      </div>
      </div>
          </div>
          <button class="btn btn-secondary">Buscar Canción</button>
        </form>
      
      </div>
     <!-- <div class="col-8">
        <p> {{artista}} </p>
        <p> {{cancion}} </p>
        <p> {{letra}} </p>
      
      </div>-->

<div class="result" v-for="letra of letras" :key="letra">
        <h2 class="text-center mb-2">{{artista}}</h2>
         <h2 class="text-center mb-2">{{cancion}}</h2>
        <div class="mt-4">{{letras}}</div>
      </div>

    </div>
  </div>
</template>

<script>
import { consumirCanciones } from "./api";

export default {
  name: "App",
  components: {},
  data() {
    return {
      artista: "",
      cancion: "",
      letra: "",
    };
  },
  methods: {
    async submit() {
      console.log('Se ejecuta el método submit')
      // 1 ejemplo
      //consumirCanciones(this.artista, this.cancion).then( letra => console.log(letra.lyrics));
      // 2 Ejemplo
      const letra = await consumirCanciones(this.artista, this.cancion);
      //console.log(letraCancion);
      
    },
    
    }
  }

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Indie+Flower&family=Space+Grotesk:wght@300&display=swap');


h1 {
  font-family: 'Indie Flower', cursive;
  color: black;
  font-size: 60px;
}

.form {
  font-family: 'Space Grotesk', sans-serif;

}
</style>

