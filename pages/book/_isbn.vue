<template>
  <section>
    <b-field label="ISBN">
      <b-input :value="book.ISBN"></b-input>
    </b-field>
    <b-field label="Nazwa">
      <b-input :value="book.Nazwa"></b-input>
    </b-field>
    <b-field label="Autor">
      <b-input :value="book.Autor"></b-input>
    </b-field>
    <b-field label="Cena">
      <b-input :value="book.Price"></b-input>
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
      const { data } = await this.$axios.put(
        '/books/' + this.book.ISBN,
        this.book
      )
      console.log(data)
    }
  }
}
</script>

<style scoped></style>
