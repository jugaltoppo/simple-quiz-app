<template>
  <div id="app">
    <Header :correctAnswer="correctAnswer" :attemptedQuestion="attemptedQuestion" />
    <Home :if="dataset.length" :dataset="dataset[index]" :increment="increment" :handleCorrect="handleCorrect"/>
  </div>
</template>

<script>

import Home from './components/Home.vue';
import Header from './components/Header.vue';

export default {
  name: 'App',
  data(){
    return {
      dataset: Array,
      index: 0,
      options: Array,
      correctAnswer: 0,
      attemptedQuestion: 0
    }
  },
  components: {
    Home,
    Header
  },
  methods: {
    increment(){
      if(this.index<9){
        this.index++
      }
    },
    handleCorrect(isCorrect){
      if(isCorrect){
        this.correctAnswer++;
      }
      this.attemptedQuestion++
    }
  },
  mounted(){
    fetch("https://opentdb.com/api.php?amount=10&category=15&type=multiple")
    .then((response)=>{
      return response.json();
    })
    .then((data)=>{
      return (this.dataset=data.results);
    })
    .catch((err)=>{
      console.log(err.response.data)
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
