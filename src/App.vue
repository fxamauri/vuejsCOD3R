<template>
  <div id="app">
    <div class="panel scores">
      <div class="score">
        <h1>Jogador</h1>
        <div class="life-bar">
          <div class="life" :class="{ danger: playerLife < 20 }" :style="{ width: `${playerLife}%` }"></div>
        </div>
        <div>{{ playerLife }}%</div>
      </div>

      <div class="score">
        <h1>Monstro</h1>
        <div class="life-bar">
          <div class="life" :class="{ danger: monsterLife < 20 }" :style="{ width: `${monsterLife}%` }"></div>
        </div>
        <div>{{ monsterLife }}%</div>
      </div>

    </div>
    <div v-if="hasResult" class="panel result">
      <div v-if="monsterLife === 0" class="win">Você GANHOU!!! :)</div>
      <div v-else class="lose">Você PERDEU!!! :(</div>
    </div>
    <div class="panel buttons">
      <template v-if="running">
        <button @click="attack(false)" class="btn attack">Ataque</button>
        <button @click="attack(true)" class="btn special-attack">Ataque Especial</button>
        <button class="btn heal">Curar</button>
        <button @click="running = false" class="btn give-up">Desistir</button>
      </template>
      <button @click="startGame" class="btn new-game">Iniciar Jogo</button>
    </div>
    <div class="panel logs"></div>
  </div>
</template>

<script>

export default {
  name: 'app',
  components: {
  },
  data() {
    return {
      running: false,
      playerLife: 100,
      monsterLife: 100
    }
  },
  computed: {
    hasResult() {
      return this.playerLife === 0 || this.monsterLife === 0
    }
  },
  methods: {
    startGame() {
      this.monsterLife = 100
      this.playerLife = 100
      this.running = true
    },
    attack(special) {

    },
    hurt() {

    },
    getRandom(min, max) {
      const value = Math.random() * (max - min) + min
      return Math.round(value)
    }
  }
}
</script>

<style lang="scss">
  html {
    font-family: 'Montserrat', 'sans-serif';
  }

  #app {
    display: flex;
    flex-direction: column;
  }

  .panel {
    margin: 10px;
    padding: 20px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.15);
  }

  .scores {
    display: flex;
  }

  .score {
    flex: 1;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    h1 {
      font-weight: 300;
      font-size: 1.6rem;
    }
  }

  .life-bar {
    width: 80%;
    height: 20px;
    border: 1px solid #AAA;

    .life {
      display: flex;
      justify-content: center;
      height: 100%;
      /*CONTROLADO NO VUE*/
      /*width: 50%;*/
      background-color: green;

      &.danger {
        background-color: red;
      }
    }
  }

  .result {
    display: flex;
    justify-content: center;
    font-size: 1.3rem;
    font-weight: 600;
  }

  .buttons {
    display: flex;
    justify-content: center;
  }

  .btn {
    padding: 5px 10px;
    margin: 0 10px;
    border-radius: 5px;
    text-transform: uppercase;
    font-size: 1.1rem;
  }

  .new-game {
    background-color: #4253fa;
    color: #fff;
  }

  .attack {
    background-color: #e51c23;
    color: #fff;
  }

  .special-attack {
    background-color: #ff9800;
    color: #000;
  }

  .heal {
    background-color: #259b24;
    color: #fff;
  }

  .give-up {
    background-color: #BBB;
    color: #000;
  }

</style>
