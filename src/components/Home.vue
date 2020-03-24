<template>
    <div>
        <h1>Quiz Box</h1>
        <p v-if="dataset===undefined">Loading...</p>
        <div v-if="dataset">
            <p> {{dataset.question}} </p>
                <p class="answer" v-for="(ans, index) in answers" :key="index" @click="selectIndex(index)" :class="[index===selectedIndex ? 'selected' : '']">{{index+1}} {{ ans }}</p>
            <button @click="checkAnswer">Submit</button><button @click="increment">Next</button>
        </div>
    </div>

</template>
<script>
import _ from 'lodash';
export default {
    props : {
        dataset : Object,
        increment: Function,
        handleCorrect: Function
    },
    data(){
        return{
            selectedIndex: null,
            answersShuffled: [],
            correctIndex: null
        }
    },
    computed: {
        answers(){
            let answers=[...this.dataset.incorrect_answers]
            answers.push(this.dataset.correct_answer);
            return answers;
        }
    },
    watch: {
        dataset: {
            immediate: true,
            handler(){
                this.selectedIndex=null,
                this.shuffleAnswer()
            }
        }
    },
    methods: {
        selectIndex(index){
            this.selectedIndex=index
        },
        shuffleAnswer(){
            let answer=[...this.dataset.incorrect_answers, this.dataset.correct_answer];
            this.answersShuffled=_.shuffle(answer);
            this.correctIndex=this.answersShuffled.indexOf(this.dataset.correct_answer)
        },
        checkAnswer(){
            let isCorrect=false;
            if(this.selectedIndex===this.correctIndex){
                isCorrect=true
            }
            this.handleCorrect(isCorrect)
        }
    }
}
</script>
<style scoped>
    .answer{
        border: 2px solid grey;
        width: 30%;
        margin: 1rem auto;
    }
    .answer:hover{
        background: grey;
        color: white;
        cursor: pointer;
    }
    .selected{
        background: lightblue;
    }
</style>