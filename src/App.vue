<template>
    <div>
      <h1>Jogo da Velha</h1>
      <h4>by Renan Toledo</h4>
      <Board />
    </div>
</template>

<script>
import Board from './main/Board'

export default {
  components: { Board }
}
</script>

<style>
  *{
    font-family: 'Roboto', sans-serif;
  }

  body{
    margin: 0;
    color: #fff;
    
  }

  #app{
    display: flex;
    justify-content: center;
    height: 100vh;
    background: linear-gradient(to right top, #051937, #004d7a, #008793, #00bf72, #a8eb12);
  }

  h1, h4{
    display: flex;
    justify-content: center;
    align-items: center;
  }



</style>
