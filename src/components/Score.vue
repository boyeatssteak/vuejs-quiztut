<template>
  <div>
    <b-jumbotron>
      <h2>Final Score:</h2>
      <p><b>{{ numCorrect }}</b> out of {{ numTotal }}</p>
      <b-button
        @click="init" 
        variant="info"
      >
        Try Again?
      </b-button>
    </b-jumbotron>
  </div>
</template>

<script>
export default {
  props: {
    numCorrect: Number,
    numTotal: Number,
    init: Function
  }
}
</script>