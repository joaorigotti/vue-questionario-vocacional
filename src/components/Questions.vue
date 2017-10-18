<template>
  <form>
    <label v-for="question of questions" :key="question.id">
      <input type="checkbox" :value="question.group" @click="selectQuestion(question)">
      <span>{{ question.text }}</span>
    </label>
  </form>
</template>

<script>
export default {
  props: ['data'],
  methods: {
    selectQuestion (question) {
      this.$emit('selectQuestion', question)
    }
  },
  data () {
    return {
      questions: []
    }
  },
  mounted () {
    fetch('static/data/questions.json')
      .then(res => res.json())
      .then(data => { this.questions = data })
      .catch(err => console.log(err))
  }
}
</script>

<style scoped>
label {
  display: block;
  cursor: pointer;
  padding: 0.3em;
  transition: all .2s ease-in-out;
}

label:hover {
  color: #999;
}
</style>
