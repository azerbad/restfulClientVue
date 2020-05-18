<template>
  <section>
    <b-field label="ISBN">
      <b-input
        v-model="book.ISBN"
        v-cleave="masks.custom"
        required
        type="text"
        validation-message="Wprowadź poprawny ISBN"
        pattern="[0-9]*[-| ][0-9]*[-| ][0-9]*[-| ][0-9]*[-| ][0-9]*"
        @input.native="onInput"
      ></b-input>
    </b-field>
    <b-field label="Nazwa">
      <b-input
        v-model="book.Nazwa"
        type="text"
        minlength="3"
        maxlength="100"
        required
      ></b-input>
    </b-field>
    <b-field label="Autor">
      <b-input
        v-model="book.Autor"
        type="text"
        minlength="5"
        maxlength="100"
        required
      ></b-input>
    </b-field>
    <b-field label="Cena">
      <b-input
        v-model="book.Price"
        type="number"
        min="0.0"
        max="1000.0"
        step=".01"
        required
      ></b-input>
    </b-field>
    <b-button type="is-light" tag="router-link" to="/">Cofnij</b-button>
    <b-button type="is-primary" @click="save">Zapisz</b-button>
  </section>
</template>

<script>
import Cleave from 'cleave.js'
const cleave = {
  name: 'cleave',
  bind(el, binding) {
    const input = el.querySelector('input')
    input._vCleave = new Cleave(input, binding.value)
  },
  unbind(el) {
    const input = el.querySelector('input')
    input._vCleave.destroy()
  }
}
export default {
  name: 'Add',
  directives: { cleave },
  data() {
    return {
      book: {},
      masks: {
        custom: {
          delimiters: ['-'],
          blocks: [3, 2, 3, 4, 1],
          numericOnly: true
        }
      }
    }
  },
  methods: {
    async save() {
      await this.$axios.$post('/books', this.book).then((response) => {
        if (response.includes('OK')) {
          this.$buefy.toast.open({
            message: 'Dane zapisane poprawnie!',
            type: 'is-success'
          })
          this.$router.push('/')
        } else {
          this.$buefy.toast.open({
            duration: 5000,
            message: `Operacja nie powiodła się`,
            position: 'is-bottom',
            type: 'is-danger'
          })
        }
      })
    },
    onInput(event) {
      this.value = event.target._vCleave.getFormattedValue()
    }
  }
}
</script>

<style scoped></style>
