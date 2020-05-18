<template>
  <section class="section">
    <p v-if="$fetchState.pending">Fetching books...</p>
    <p v-else-if="$fetchState.error">
      Error while fetching books: {{ $fetchState.error.message }}
    </p>
    <b-table :data.sync="data">
      <template slot-scope="props">
        <b-table-column field="ISBN" label="ISBN" width="250">
          {{ props.row.ISBN }}
        </b-table-column>
        <b-table-column field="Nazwa" label="Nazwa" width="300">
          {{ props.row.Nazwa }}
        </b-table-column>
        <b-table-column field="Autor" label="Autor" width="300">
          {{ props.row.Autor }}
        </b-table-column>
        <b-table-column field="Price" label="Cena" width="150">
          {{ props.row.Price }} PLN
        </b-table-column>
        <b-table-column field="akcja" label="Akcje" width="300">
          <b-button
            tag="router-link"
            type="is-info"
            :to="/book/ + props.row.ISBN"
            ><b-icon icon="square-edit-outline"
          /></b-button>
          <b-button type="is-danger" @click="deleteBook(props.row)"
            ><b-icon icon="delete"
          /></b-button>
        </b-table-column>
      </template>
    </b-table>
  </section>
</template>

<script>
export default {
  name: 'HomePage',
  async fetch() {
    const { data } = await this.$axios.get('/books')
    this.data = data
  },
  data() {
    return {
      data: []
    }
  },
  methods: {
    async deleteBook(book) {
      await this.$axios.$delete('/books/' + book.ISBN)
      this.data = this.data.filter(function(element) {
        return element.ISBN !== book.ISBN
      })
    }
  },
  fetchOnServer: false
}
</script>
