<template>
<div>
  <h1>{{title}}</h1>
  <p>wellcome...</p>
  <input type="text" ref="name">
  <button @click="handleClick">Click me</button>
  <!-- a tag teleport joga a div para o index.html para declarar usamos o atributo 'to' e o valor .modals assim ele será renderizado no index.html  -->
  <teleport to=".modals" v-if="showModal">
  <!-- theme="sale" estamos passando uma classe dinamicamente via props para nossa tag especifica. -->
    <Modal :header="header" :text="text" theme="sale" @close="toggleModal"> 
    <!-- o @close é um evento passado pelo componente filho via $emit que é disparada onde é declarado via função na tag.-->
    <!-- Componentes que começam com letra maiuscula não dão conflito com palavras reservadas do HTML -->
      <p>texto passado via slot do componente pai para o componente filho nesse espacinho reservado</p>
        <template v-slot:links>
          <a href="#">Sign Up now</a>
          <a href="#">more info</a>  
        </template>
    </Modal>
  </teleport>
  <button @click.alt="toggleModal">Show Modal (alt)</button>
  <!-- esse click.alt ele faz um prevent default e acrescenta a regra de que só será disparado o evento quando a tecla alt estiver pressionada. -->
</div>
</template>

<script>
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {Modal},
  data(){
    return {
      title: 'my first vue app :)',
      header: 'Sign in for offers!',
      text: 'Grab your ninja swag of half of the price!',
      showModal: false
    }
  },
  methods: {
    handleClick(){
      console.log(this.$refs.name) //refs substuem o queryselector nos dando acesso aos elementos
      //esse console.log(está me retornando e selecionando o input no console.)
      this.$refs.name.classList.add('active') //o classList é uma propriedade de leitura que nos retorna uma coleção ativa dos atributos de classe do elemento
      //o metodo add() adiciona valores de classes especificados ao elemento.
      //resumindo esse metodo está adicionando a classe active no elemento input que foi referencialdo ($refs) por name (ref="name").
      this.$refs.name.focus() //o metodo focus dá fogo a um elemento html.
      //lembrar de usar o $refs pois é uma palavra registrada para o vue.js
    },
    toggleModal(){
      this.showModal = !this.showModal
    }
  }
}
</script>

<style>
#app .modals {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
