<template>
  <div class="container mt-4">
    <h1 class="text-center mt-5 mb-5">Busca-Canciones</h1>
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
          <button class="btn">Buscar Canción</button>
        </form>
      
      </div>
     <!-- <div class="col-8">
        <p> {{artista}} </p>
        <p> {{cancion}} </p>
        <p> {{letra}} </p>
      
      </div>-->

      <div class="result">
        <h2 class="text-center mb-2">{{artista}}</h2>
         <h2 class="text-center mb-2">{{cancion}}</h2>
        <div class="mt-4">{{letra}}</div>
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
      this.letra = letra.lyrics;
      console.log(letra.lyrics);
      
    },
    
    }
  }

</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Chakra+Petch:wght@300&family=Space+Grotesk:wght@300&display=swap');




h1 {
  font-family: 'Chakra Petch', sans-serif;
  color: rgb(91, 91, 91);
  font-size: 60px;
}

label {
  font-size: 22px;
}
input {
  border: 1px solid #e6a9e6;
}
.card {
  margin-top: 5px;
  background: #a7baff;
  border: 1px solid #e6a9e6;
  font-size: 5px;
}
h6 {

  color: white;
}

.formu {
  font-family: 'Space Grotesk', sans-serif;

}

.btn {
  background: #e6a9e6;
  box-shadow: 0 0px 10px 0 rgba(0,0,0,0.4);
  color: black;
  border: 1px solid #93cb8d;
}

.result {
  font-family: 'Space Grotesk', sans-serif;
  margin-bottom: 50px;
}
</style>

