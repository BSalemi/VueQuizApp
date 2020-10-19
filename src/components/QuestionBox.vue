<template>
    <div class="question-box-container">
      <b-jumbotron >

        <template v-slot:lead>
          {{ currentQuestion.question }}
        </template>

        <hr class="my-4">

        <b-list-group>
          <b-list-group-item 
            v-for="(answer, index) in answers" 
            :key="index"
            @click="selectAnswer(index)"
          >
             {{answer}}
          </b-list-group-item>
        </b-list-group>

        <b-button variant="primary" href="#">Submit</b-button>
        <b-button @click="nextQuestion" variant="success" href="#">Next Question </b-button>
      </b-jumbotron>
  </div>
</template>

<script>
  export default {
    props: {
      currentQuestion: Object,
      nextQuestion: Function
    },
    data(){
      return {
        selectedIndex: null
      }
    },
    computed: {
      answers(){
        let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)

        return answers
      }
    },
    methods: {
      selectAnswer(index){
        this.selectedIndex = index
      }
    }
  }
</script>

<style scoped>
  .list-group{
    margin-bottom: 15px;
  }

  .btn {
    margin: 0 5px;
  }
</style>