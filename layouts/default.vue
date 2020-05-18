<template>
  <div>
    <nav
      class="navbar header has-shadow is-primary"
      role="navigation"
      aria-label="main navigation"
    ></nav>

    <section class="main-content columns">
      <aside class="column is-2 section">
        <p class="menu-label is-hidden-touch">
          Menu
        </p>
        <ul class="menu-list">
          <li v-for="(item, key) of items" :key="key">
            <nuxt-link :to="item.to" exact-active-class="is-active">
              <b-icon :icon="item.icon" /> {{ item.title }}
            </nuxt-link>
          </li>
        </ul>
      </aside>

      <div class="container column is-10">
        <nuxt />
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          title: 'Spis',
          icon: 'home',
          to: { name: 'index' }
        },
        {
          title: 'Dodaj ksiażkę',
          icon: 'plus',
          to: { name: 'add' }
        },
        {
          title: 'Wyszukaj',
          icon: 'magnify',
          to: { name: 'search' }
        }
      ]
    }
  }
}
</script>
<style>
.container {
  margin-top: 2rem;
}
</style>
