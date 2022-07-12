<template>
    <div>
        <h2>Editar filme</h2>

        <div class="form-group">
            <label>Título:</label>
            <input type="text" class="form-control" 
            placeholder="Insira o título" :value="filme.titulo"  
            @input="filmeSelecionado={propriedade: 'titulo', 
            valor:$event.target.value}">
        </div>

         <div class="form-group">
            <label>Título:</label>
            <input type="text" class="form-control"
             placeholder="Insira o ano" 
             :value="filme.ano" 
             @input="filmeSelecionado={propriedade: 
             'ano', valor:$event.target.value}">
        </div>
        
        <button @click="send">Editar</button>
    </div>
</template>

<script>
import {eventBus} from './../main'


export default {
      data(){
        return {
            filmeLocal: this.filme
        }
      },
      methods: {
        send(){
          eventBus.$emit('salvar', this.filmeLocal)
        },
        
      },

      props: {
         filme: {
            type: Object,
            required: true
         }
      },

       computed: {
        filmeSelecionado: {
            set(dados){
              this.filmeLocal = Object.assign(
                {},
                this.filmeLocal,
                {[dados.propriedade]: dados.valor}
              )
            },
            get(){
               return this.filme
            }

        }
      },
      watch: {
        filme(novoFilme){
            this.filmeLocal = Object.assign({}, novoFilme)
        }
      }

}
</script>
