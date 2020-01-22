<template>
  <b-container>
    <template v-if="recipes">
      <b-row v-for="recipe in recipes.data" :key="recipe.id">
        <b-col xl="12">
          <h1>
            <b-btn @click="open(recipe.links.self.href)">{{
              recipe.attributes.title
            }}</b-btn>
          </h1>
        </b-col>
      </b-row>
      <b-row>
        <b-col>
          <div class="posts__body" />
        </b-col>
      </b-row>
    </template>
  </b-container>
</template>

<script>
export default {
  components: {},
  async asyncData({ app }) {
    const data = await app.$axios
      .get('/api/recipes', {})
      .then(({ data: { data } }) => ({ recipes: { data } }))
      .catch((e) => {
        if (e) return e
      })

    console.log(JSON.stringify(data))

    return data
  },
  methods: {
    async open(path) {
      if (!path) return

      const data = await this.$axios
        .$get(path, {})
        .then(({ data }) => {
          console.log(data)
        })
        .catch((e) => {
          if (e) return e
        })

      console.log(data)
    }
  }
}
</script>
