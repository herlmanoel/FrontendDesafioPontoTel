<template>
  <div id="app">
    <Cotacao/>
  </div>
</template>

<script>
import Cotacao from './components/Cotacao';

export default {
  name: 'App',
  components: {
    Cotacao
  }
}
</script>

<style>
  * {
    padding:0;
    margin:0;
    list-style:none;
    border:0;
    box-sizing: border-box;
    padding: 0;
  }
  body, html {
    width: 100vw;
    height: 100vh;
    background-color: #FDFDFD;
  }
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    width: 100vw;
    height: 100vh;
    display: flex;
    margin: 0 auto;
    align-items: center !important;
    justify-content: center;
  }
</style>
