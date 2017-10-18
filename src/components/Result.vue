<template>
  <div class="container">
    <h2>Resultado</h2>
    <p>
      Você é mais apto para: {{ result.name }} <br>
      Podendo seguir carreira em: {{ result.carrers }}
    </p>
  </div>
</template>

<script>

export default {
  props: ['group'],
  computed: {
    result () {
      if (!this.group) {
        return {
          name: '',
          carrers: ''
        }
      }

      return this.group
    }
  }
}
</script>

<style scoped>
.container {
  position: fixed;
  width: 80%;
  height: 160px;
  bottom: 0;
  background: rgba(255, 255, 255, 0.9);
  box-shadow: 0 -40px 20px rgba(255, 255, 255, 0.8);
}
</style>
