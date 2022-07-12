<template>
  <div class="row">

    <!-- coluna 1 -->
    <div class="col-8">

      <h2>Filmes</h2>

      <div class="list-group list-group-flush">
       
         <FilmesListaIten v-for="filme in filmes" :key="filme.id" :filme="filme" @selecionarFilme="filmeSelecionado = $event" :class="aplicarEstilo(filme)"/> 
         
      </div>
    </div>

    <!-- coluna 2 -->
    <ul class="col-4">

      <FilmesListaItenInfo v-if="!editar" @mandar="editarFilme"/>
      <FilmesListaItenEdit v-else :filme="filmeSelecionado"/>

    </ul>

  </div>
</template>

<script>

import FilmesListaIten from './FilmesListaIten.vue'
import FilmesListaItenInfo from './FilmesListaItenInfo.vue'
import FilmesListaItenEdit from './FilmesListaItenEditar.vue'
import {eventBus} from './../main'

export default {
  
  data(){
    return {
        filmes: 
        [{id: 1, titulo:'Vingadores', ano: 2012}, 
        {id: 2, titulo:'homem formiga', ano: 2016}, 
        {id: 3, titulo:'pantera', ano: 2018}],
        editar: false,
        filmeSelecionado: undefined
        
    }
  },
  methods: {
    aplicarEstilo(filmeIterado) {
     return {active: this.filmeSelecionado && this.filmeSelecionado.id === filmeIterado.id}
    },
    editarFilme(filme){
      this.editar = true
      this.filmeSelecionado = filme
    },
     atualizarFilme(filmeAtualizado){  
      let index = this.filmes.findIndex(filme => filme.id === filmeAtualizado.id) 
      this.filmes.splice(index, 1, filmeAtualizado)
      this.filmeSelecionado = undefined
      this.editar = false
    }
  },
  components: {
    FilmesListaIten,
    FilmesListaItenInfo,
    FilmesListaItenEdit
  },

 

  created(){
   
    eventBus.$on('selecionarFilme', filmeSelecionado => {
      this.filmeSelecionado = filmeSelecionado
    }) 
    eventBus.$on('salvar',  this.atualizarFilme)
  }
}
</script>
