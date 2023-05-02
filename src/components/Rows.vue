<template>
  <div class="rows">
      <div v-html="canvasBoard.a1" @click="changeHTML"></div>
      <div v-html="canvasBoard.a2" @click="changeHTML"></div>
      <div v-html="canvasBoard.a3" @click="changeHTML"></div>
      <div v-html="canvasBoard.b1" @click="changeHTML"></div>
      <div v-html="canvasBoard.b2" @click="changeHTML"></div>
      <div v-html="canvasBoard.b3" @click="changeHTML"></div>
      <div v-html="canvasBoard.c1" @click="changeHTML"></div>
      <div v-html="canvasBoard.c2" @click="changeHTML"></div>
      <div v-html="canvasBoard.c3" @click="changeHTML"></div>
      <div v-html="canvasBoard.winnerMessage" @click="changeHTML" :class="{ messageClass: active }"></div>
      
  </div>
</template>

<script>

export default {
    data() {
        return {
           canvasBoard: {
            a1: '<canvas class="a1"></canvas>',
            a2: '<canvas class="a2"></canvas>',
            a3: '<canvas class="a3"></canvas>',
            b1: '<canvas class="b1"></canvas>',
            b2: '<canvas class="b2"></canvas>',
            b3: '<canvas class="b3"></canvas>',
            c1: '<canvas class="c1"></canvas>',
            c2: '<canvas class="c2"></canvas>',
            c3: '<canvas class="c3"></canvas>',
            winnerMessage: '',
            contador: 1
            },
            winnersCombination: [
                ['a1', 'a2', 'a3'],
                ['b1', 'b2', 'b3'],
                ['c1', 'c2', 'c3'],
                ['a1', 'b1', 'c1'],
                ['a2', 'b2', 'c2'],
                ['a3', 'b3', 'c3'],
                ['a1', 'b2', 'c3'],
                ['a3', 'b2', 'c1']
            ],
            winnerPlayer: {
                combinationsX: [],
                combinationsO: []
            },
            active: true
        }
    },
    methods: {
        changeHTML(event){

            let canvasBoard = this.canvasBoard
            let contador = canvasBoard.contador++
            let combinationsX = this.winnerPlayer.combinationsX
            let combinationsO = this.winnerPlayer.combinationsO
            let winnersCombination = this.winnersCombination

            const boardPosition = event.path[0].className
            
            for(let i in canvasBoard){
                if( boardPosition == i){
                    if(contador % 2){
                        canvasBoard[i] = '<div class="x"><img alt="X"></div>'
                        combinationsX.push(boardPosition)
                    }else{
                        canvasBoard[i] = '<div class="o"><img alt="O"></div>'
                        combinationsO.push(boardPosition)
                    }
                    
                }
            }

            let winnerX = combinationsX.sort()
            let winnerO = combinationsO.sort()
            let winnerMessage = ''

            for(let i in winnersCombination){
                let combinations = winnersCombination[i]
                const winnerFinal = combinations.every(value => {
                    return winnerX.includes(value)
                })
                if(winnerFinal){
                    winnerMessage = 'X'
                    canvasBoard.winnerMessage = 
                    `<div class="winnerMessage">
                        <p>
                            Jogador "${winnerMessage}" Venceu
                        </p>
                        <button onclick="window.location.reload()">
                            Reiniciar
                        </button>
                    </div>`
                    this.active = false
                  } else if(!winnerFinal && contador === 9){
                      canvasBoard.winnerMessage = 
                      `<div class="winnerMessage">
                        <p>
                            Empate!
                        </p>
                        <button onclick="window.location.reload()">
                            Reiniciar
                        </button>
                    </div>`
                    this.active = false
                  }
            }
            
            for(let i in winnersCombination){
                let combinations = winnersCombination[i]
                const winnerFinal = combinations.every(value => {
                    return winnerO.includes(value)
                })
                if(winnerFinal){
                    winnerMessage = 'O'
                    canvasBoard.winnerMessage = 
                    `<div class="winnerMessage">
                        <p>
                            Jogador "${winnerMessage}" Venceu
                        </p>
                        <button onclick="window.location.reload()">
                            Reiniciar
                        </button>
                    </div>`
                    this.active = false
                  } else if(!winnerFinal && contador === 9){
                     canvasBoard.winnerMessage = 
                      `<div class="winnerMessage">
                        <p>
                            Empate!
                        </p>
                        <button onclick="window.location.reload()">
                            Reiniciar
                        </button>
                    </div>`
                    this.active = false
                  }
            }
            
        }
    }
}
  
</script>

<style>

    .rows{
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        justify-content: space-between;
        
        
    }
    canvas{
        width: 120px;
        height: 120px;
        border: 3px solid white;
        margin-bottom: 5px;
        background: white;

    }

    .messageClass{
        display: none;
    }

    .x img{
        content: url(../assets/imgs/marker-x.png);
        margin-bottom: 5px;
    }

    .o img{
        content: url(../assets/imgs/marker-o.png);
        margin-bottom: 5px;
    }

    .winnerMessage{
        display: flex;
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        justify-content: center;
        align-items: center;
        background-color: rgb(0, 0, 0, 0.6);
        flex-direction: column;
        font-size: 50px;
    }

    .winnerMessage button{
        font-size: 2.5rem;
        background-color: #db3362;
        padding: 10px 15px;
        cursor: pointer;
        border-radius: 10px;
        border: none;
        margin-top: 16px;
        color: white;
    }

    .winnerMessage button:hover{
        background-color: white;
        color:#db3362;
    }

</style>