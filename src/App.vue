<template>
<h1>Ninja reaction timer</h1>


<button @click='start' :disabled='isPlaying' v-if='!againBtn'> {{isPlaying ? 'Playing' : 'Play'}} </button>
<button @click='start' :disabled='isPlaying' v-if='againBtn'>  {{isPlaying ? 'Playing' : 'Play again'}} </button>

<Block v-if="isPlaying" :delay="delay" @end="endGame"  />
<Results v-if="showResults" :score="score"/>
</template>

<script>
import Block from './components/Block.vue'
import Results from './components/Results.vue'

export default {
  name: 'App',
  components: { Block, Results },
  data(){
    return{
      isPlaying: false,
      delay: null,
      score: null,
      showResults: false,
      againBtn: false
    }
  },
  methods:{
    start(){
      this.delay = Math.random() * 5000
      this.isPlaying = true
      this.showResults = false
    },
    endGame(reactionTime){
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
      this.againBtn = true
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
button{
  background: rgb(58, 48, 194);
  color:white;
  padding: 5px 30px;
  border-radius: 4px;
  border:none;
  font-size: 16px;
  letter-spacing: 1px;
  cursor:pointer;
  margin: 10px;
}
button:disabled{
  opacity: 0.2;
  cursor: not-allowed
}
button:hover:enabled{
   padding: 5px 20px;
}
</style>