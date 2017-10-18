<template>
  <div id="app">
    <h1>Teste vocacional</h1>
    <questions @selectQuestion="selectQuestion" />
    <result :group="group" />
  </div>
</template>

<script>
import Questions from './components/Questions'
import Result from './components/Result'
import groups from './groups'

const selectedQuestions = []

function scoreGroup (question) {
  const index = selectedQuestions.findIndex(q => q.id === question.id)
  const group = question.group

  if (index === -1) {
    groups[group].points += 1
  } else {
    groups[group].points -= 1
  }

  return index
}

function addQuestion (question) {
  selectedQuestions.push(question)
}

function removeQuestion (index) {
  selectedQuestions.splice(index, 1)
}

function chooseGroup () {
  let points = 0
  let selectedGroup

  Object.keys(groups).forEach(group => {
    if (points < groups[group].points) {
      points = groups[group].points
      selectedGroup = groups[group]
    }
  })

  return selectedGroup
}

export default {
  name: 'app',
  components: {
    Questions,
    Result
  },
  data () {
    return {
      group: {}
    }
  },
  methods: {
    selectQuestion (question) {
      const index = scoreGroup(question)

      if (index === -1) {
        addQuestion(question)
      } else {
        removeQuestion(index)
      }

      this.group = chooseGroup()
    }
  }
}
</script>

<style>
#app {
  width: 80%;
  margin: 0 auto;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  margin-bottom: 200px;
  position: relative;
}
</style>
