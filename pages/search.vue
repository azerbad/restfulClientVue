<template>
  <section>
    <p v-if="$fetchState.pending">Fetching books...</p>
    <p v-else-if="$fetchState.error">
      Error while fetching books: {{ $fetchState.error.message }}
    </p>
    <b-field label="Search..." label-position="on-border">
      <b-input
        v-model="query"
        placeholder="Szukaj..."
        type="search"
        expanded
        @input="search"
      ></b-input>
      <p class="control">
        <b-button class="button is-primary" @click="search">Szukaj</b-button>
      </p>
    </b-field>
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
      </template>
    </b-table>
  </section>
</template>

<script>
export default {
  name: 'Search',
  async fetch() {
    const { data } = await this.$axios.get('/books')
    this.data = data
  },
  data() {
    return {
      data: [],
      query: ''
    }
  },
  methods: {
    async search() {
      const { data } = await this.$axios.get('/books?q=' + this.query)
      this.data = data
    }
  },
  fetchOnServer: false
}
</script>

<style scoped></style>
