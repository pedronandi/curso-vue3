<template>
  <div>
    <h1 :style="{ textDecoration: decoration }">Hello {{ name }}</h1>
    <input type="text" v-model="name">
    <br>
    <a :href="link">Link pro curso!</a>
  </div>
</template>

<script>
export default {
  data: () => ({ /*data: two-way binding: O model interage com a view e vice-versa*/
    name: 'Pedro',
    link: 'https://treinamento.vuejsbrasil.org',
    decoration: 'underline'
  })
}
</script>