<style scoped>
::placeholder {
  @apply rfs-text-lg text-gray-400 font-light;
}
</style>
<template>
  <div id="search_div" class="w-full max-w-1200 mx-auto flex flex-row justify-end items-center search_div" style="top:20px;">
    <input ref="input" class="w-100 text-xl text-black text-xl border border-gray-200 focus:outline-none focus:shadow focus:border-gray-400 rounded px-3 py-2 appearance-none leading-normal bg-white" placeholder="Search Blog" type="search" @input="search" @focus="search" @blur="search" @keydown.esc.enter="$refs.input.blur()" v-model="q" />
    <a v-if="value" href="#current_post" class="rfs-text-xl float-left text-black border-gray-200 w-100" v-text="`${value.length} results`" />
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
          'node:name',
          'node:position'
        ]
      }
    })
    this.index.add(this.$static.allAuthor.edges)

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
    query Author {
    allAuthor {
    edges {
    node {
    id
    name
    date(format: "MMMM D YYYY")
    path
    authorAbout
    name
    authorImage
    path
    }
    }
    }
    }
</static-query>
