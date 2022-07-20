<template>
  <div id="app" class="container">
    <h1>Components dinamico</h1>

    <button @click="componenteSelecionado = 'Home'">Home</button>
    <button @click="componenteSelecionado = 'Sobre'">Sobre</button>
    <button @click="componenteSelecionado = 'PostsLista'">Posts</button>
    <button @click="componenteSelecionado = 'Assincrono'">Assincrono</button>

     
    <keep-alive max="2">
      <component :is="componenteSelecionado" v-bind="componentsSelecionado"></component>

    </keep-alive>
  </div> 
</template>

<script>
import PostsLista from './components/PostsLista.vue'
import Home from './components/Home.vue'
import Sobre from './components/SobreComponent.vue'




export default {
  components: {
    Home,
    Sobre,
    PostsLista,
    Assincrono: () => ({
      component: new Promise((resolve, rejects) => 

      setTimeout(() => {
        resolve(import('./components/Assincrono.vue'))
      }, 2000)),

      loading: {template: "<p>Carregando</p>"},
      error: {template: '<p>Erro ao Carregar component</p>'},
      delay: 200,
      timeout: 3000
    })
    
    
  },
  data(){
    return{
      componenteSelecionado: 'Home',
      posts: [{
        id: 1,
        titulo: 'Vue é bom?',
        conteudo: 'sim, ele pode ser de grande uso',
        autor: 'Donovan'
      }, {
        id: 2,
        titulo: 'Js ou react direto?',
        conteudo: 'aprofunde o js primeiro, para entender como tudo funciona e depois um framework',
        autor: 'Josue'
      }, ]
    }
  },
  computed: {
    componentsSelecionado(){
      return this.componenteSelecionado === 'PostsLista' ? {posts: this.posts}: {} 
    }
  }
}
</script>

<style scoped>
.container{
  width: 900px;
  margin: 0 auto;
}

.conteudo-paragrafo{
    color: red;
}
</style>