<template>
  <section>
    <b-field label="ISBN">
      <b-input v-model="book.ISBN"></b-input>
    </b-field>
    <b-field label="Nazwa">
      <b-input v-model="book.Nazwa"></b-input>
    </b-field>
    <b-field label="Autor">
      <b-input v-model="book.Autor"></b-input>
    </b-field>
    <b-field label="Cena">
      <b-input v-model="book.Price"></b-input>
    </b-field>
    <b-button type="is-light" tag="router-link" to="/">Cofnij</b-button>
    <b-button type="is-primary" @click="save">Zapisz</b-button>
  </section>
</template>

<script>
export default {
  name: 'Book',
  async fetch() {
    const { data } = await this.$axios.get('/books/' + this.$route.params.isbn)
    this.book = data
  },
  data() {
    return {
      book: {},
      msg: ''
    }
  },
  methods: {
    async save(event) {
      console.log(this.book)
      await this.$axios
        .put('/books/' + this.book.ISBN, this.book)
        .then((response) => {
          if (response.status === 200) {
            this.$router.push('/')
          } else {
            // pass
          }
        })
    }
  }
}
</script>

<style scoped></style>
