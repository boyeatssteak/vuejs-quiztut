<template>
  <div id="app">
    <Header
      :numCorrect="numCorrect"
      :numTotal="numTotal"
    />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions.length && index < 10"
            :currentQuestion="questions[index]"
            :next="next"
            :increment="increment"
          />
          <Score
            v-if="questions.length && index >= 10"
            :numCorrect="numCorrect"
            :numTotal="numTotal"
            :init="init"
          />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<!-- v-if directive in QuestionBox above causes element not to render until the questions prop has been populated -->

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import Score from './components/Score.vue'

export default {
  name: 'app',
  components: {
    Header,
    QuestionBox,
    Score
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    }
  },
  methods: {
    next() {
      this.index++
    },
    increment(isCorrect) {
      if(isCorrect) {
        this.numCorrect++
      }
      this.numTotal++
    },
    init() {
      console.log("resetting")
      this.questions = []
      this.index = 0
      this.numCorrect = 0
      this.numTotal = 0

      fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple', {
        // https://opentdb.com/api_config.php
      method: 'get'
    })
      .then((response) => {
        return response.json()
      })
      .then((jsonData) => {
        this.questions = jsonData.results;
      })
    }
  },
  mounted: function() {
    this.init()
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
