<template>
  <section>
    <p v-html="data"></p>
  </section>
</template>

<script>
export default {
  name: 'Info',
  async fetch() {
    const { data } = await this.$axios.get('/info')
    this.data = data
  },
  data() {
    return {
      data: ''
    }
  }
}
</script>

<style scoped></style>
