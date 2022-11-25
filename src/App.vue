// O App Vue é o componente central que gerenciará toda a aplicação

<template>
  <div id="App">
    <Calculator msg="Calculator Vue JS" />
  </div>
</template>

<script>// no import você importa como uma classe e indica a origem do documento:
  import Calculator from './components/Calculator.vue'

  // Em export default, na parte de components, eu preciso colocar em evidência a classe que foi importada:
  export default {
    name: 'App',
    // segue aqui os componentes criados e importados para o App(que é o componente principal):
    components: {
      Calculator
    } 
  }

</script>

<style>
  #App {
    color:#02bb68;
  }
</style>