<template>
    <div class="question-box-container">
      <b-jumbotron >

        <template v-slot:lead>
          {{ currentQuestion.question }}
        </template>

        <hr class="my-4">

        <p>
          List of Answers
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
    }
  }
</script>