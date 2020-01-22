<template>
  <b-container>
    <b-row>
      <b-col xl="12">
        <h1>{{ title }}</h1>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <div v-html="body" class="posts__body" />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
export default {
  components: {},
  async asyncData({ app }) {
    const data = await app.$axios
      .get(
        '/api/recipes/811ae8e5-0b28-418f-ab23-ea429d690495?resourceVersion=id%3A15',
        {}
      )
      .then((res) => {
        return {
          title: res.data.data.attributes.title,
          body: res.data.data.attributes.instructions
        }
      })
      .catch((e) => {
        if (e) return e
      })

    return data
  }
}
</script>

<style scoped></style>
