<style scoped>
::placeholder {
  @apply rfs-text-lg text-gray-400 font-light;
}
</style>
<template>
  <div class="w-full max-w-1200 mx-auto flex flex-row justify-end items-center">
    <span v-if="value" class="rfs-text-2xl float-left w-1/4" v-text="`${value.length} results`" />
    <input ref="input" class="w-3/4 text-xl text-black text-xl border border-gray-200 focus:outline-none focus:shadow focus:border-gray-400 rounded px-3 py-2 appearance-none leading-normal bg-white" placeholder="Search Blog" type="search" @input="search" @focus="search" @blur="search" @keydown.esc.enter="$refs.input.blur()" v-model="q" />
  </div>
</template>

<script>
import Flexsearch from 'flexsearch'

export default {
  props: ['value'],
  data: () => ({
    index: null,
    q: ''
  }),
  beforeMount () {
    this.index = new Flexsearch({
      doc: {
        id: 'node:id',
        field: [
          'node:title',
          'node:content'
        ]
      }
    })
    this.index.add(this.$static.allBlog.edges)

    document.onkeyup = (e) => {
      if (e.which === 191) this.$refs.input.focus()
    }
  },
  methods: {
    search () {
      let res
      if (this.index === null || (this.$refs.input !== document.activeElement && this.q === '')) res = null
      else if (this.q.length < 1) res = []
      else res = this.index.search({ query: this.q })
      this.$emit('input', res)
    }
  }
}
</script>

<static-query>
  query Blog {
    allBlog {
      edges {
        node {
          id
          title
          date(format: "MMMM D YYYY")
          path
          coverImage
          content
        }
      }
    }
  }
</static-query>
