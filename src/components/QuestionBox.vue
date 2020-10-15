<template>
    <div class="question-box-container">
      <b-jumbotron >

        <template v-slot:lead>
          {{ currentQuestion.question }}
        </template>

        <hr class="my-4">

        <p v-for="(answer, index) in answers" :key="index">
          {{answer}}
        </p>

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
    computed: {
      answers(){
        let answers = [...this.currentQuestion.incorrect_answers]
        answers.push(this.currentQuestion.correct_answer)

        return answers
      }
    }
  }
</script>