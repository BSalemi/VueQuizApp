<template>
    <div class="question-box-container">
      <b-jumbotron >

        <template v-slot:lead>
          {{ currentQuestion.question }}
        </template>

        <hr class="my-4">

        <b-list-group>
          <b-list-group-item 
            v-for="(answer, index) in shuffledAnswers" 
            :key="index"
            @click="selectAnswer(index)"
            :class="answerClass(index)"
          >
             {{answer}}
          </b-list-group-item>
        </b-list-group>

        <b-button
          variant="primary"
          @click="submitAnswer"
          :disabled="selectedIndex === null || answered"
        >
          Submit
        </b-button>
        <b-button @click="nextQuestion" variant="success">
          Next Question
        </b-button>
      </b-jumbotron>
  </div>
</template>

<script>

  import _ from 'lodash'

  export default {
    props: {
      currentQuestion: Object,
      nextQuestion: Function,
      increment: Function
    },
    data(){
      return {
        selectedIndex: null,
        shuffledAnswers: [],
        correctIndex: null,
        answered: false
      }
    },
    computed: {
      answers(){
        let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)

        return answers
      }
    },
    watch: {
      currentQuestion: {
        immediate: true,
        handler(){
        this.selectedIndex = null
        this.answered = false
        this.shuffleAnswers()
        }
      }
    },
    methods: {
      selectAnswer(index){
        this.selectedIndex = index
      },
      submitAnswer(){
        let isCorrect = false

        if (this.selectedIndex === this.correctIndex){
          isCorrect = true
        }

        this.answered = true 

        this.increment(isCorrect)
      },
      shuffleAnswers(){
        let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
        this.shuffledAnswers = _.shuffle(answers)
        this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
      },
      answerClass(index){
        const {answered, selectedIndex, correctIndex} = this
        let answerClass = '';

        if(!answered && selectedIndex === index){
          answerClass = 'selected'
        } else if(answered && correctIndex === index){
          answerClass = 'correct'
        } else if (answered && selectedIndex === index && correctIndex !== index){
          answerClass = 'incorrect'
        }

        return answerClass
      }
    }
  }
</script>

<style scoped>
  .list-group{
    margin-bottom: 15px;
  }

  .list-group-item:hover{
    background: #eee;
    cursor: pointer;
  }

  .btn {
    margin: 0 5px;
  }

  .selected {
    background-color: lightblue;
  }

  .correct {
    background-color: lightgreen;
  }

  .incorrect {
    background-color: red;
  }
</style>