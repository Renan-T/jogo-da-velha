<template>
  <div class="board">
      <Rows />
  </div>
</template>

<script>
import Rows from '../components/Rows'

export default {
    components: { Rows }
}
</script>

<style>
.board{
    height: 390px;
    width: 390px;
}
</style>