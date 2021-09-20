<template lang='pug'>
div
  TntContent(v-if='page && !Array.isArray(page)' :article='page')
  FizzBuzz
</template>

<script>
export default {
  layout: 'docs',

  async asyncData ({ $content }) {
    const slug = 'fizzbuzz'

    const page = await $content(slug)
      .where({ draft: { $ne: true } })
      .sortBy('date', 'desc')
      .fetch()

    return { slug, page }
  }
}
</script>
