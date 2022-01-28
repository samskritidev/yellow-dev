<style scoped>
body {
  background: rgba(13,23,28,1);
}
.hero {
  background-size: cover;
  position: relative;
  &:after {
    content: '';
    @apply absolute top-0 bottom-0 left-0 right-0;
    background: linear-gradient(0deg, rgba(13,23,28,1) 0%, rgba(13,23,28,0) 70%);
  }
}

.blog {
  margin-bottom: 0;
}

.blog-bg {
  background-image: url(/uploads/new-pattern.svg);
  background-position: top right;
  background-repeat: no-repeat;
  background-size: 100%;
}
</style>

<template>
  <Layout>

    <section class="hero" :style="[$page.blog.coverImage ? {backgroundImage: 'url(' + $page.blog.coverImage + ')' } : {'backgroundImage': 'url(/assets/images/generic-bg.svg)'}]">
      <div class="max-w-1000 w-full mx-auto py-24 z-10">
        <div class="relative border-b-0 border-t-0 border-l-4 border-r-0 border-yellow1 pl-8">
          <h1 class="w-full md:w-1/2 rfs-text-6xl leading-none text-white font-semibold" v-html="$page.blog.title" />
          <p v-if="$page.blog.author" class="text-white pl-1" v-html="$page.blog.author" />
        </div>
      </div>
    </section>

    <section class="bg-gray-700 pt-0 pb-2 px-6">
      <div class="flex w-full max-w-1000 mx-auto mb-4  bg-transparent">
        <span class="self-start text-yellow1 leading-none" v-html="$page.blog.date" />
          <template v-if="$page.blog.categories">
            <span class="inline-block border-l-2 border-teal mx-4"></span>
            <a v-for="(category) in $page.blog.categories" :key="category.id" v-text="category.title === 'yellowbrick and tpc-ds' ? 'Yellowbrick and TPC-DS' : category.title" :href="`/blog/category/${category.title}`" class="capitalize text-yellow1 leading-none mr-2 inline" />
          </template>
        <span class="self-start ml-auto leading-none"><a href="/blog" class="text-teal hover:text-yellow1">Back to Blog > </a></span>
      </div>
    </section>

    <section class="bg-gray-700 pb-24 px-6 xl:px-0 blog">
      <div class="flex flex-col max-w-1000 bg-white p-12 w-full mx-auto relative">
        <!-- <span class="accent"></span> -->
        <VueRemarkContent />
      </div>
    </section>
  </Layout>
</template>

<script>
export default {
  metaInfo() {
    return {
      title: this.$page.blog.title,
      meta: [
        {
          key: 'description',
          name: 'description',
          content: this.$page.blog.description
        },
        {
          key: 'og:title',
          name: 'og:title',
          content: this.$page.blog.title,
        },
        {
          key: 'og:description',
          name: 'og:description',
          content: this.$page.blog.description,
        },
        {
          key: 'og:url',
          name: 'og:url',
          content: 'https://www.yellowbrick.com' + this.$page.blog.path,
        },
        {
          key: 'og:image',
          name: 'og:image',
          content: 'https://www.yellowbrick.com' + this.$page.blog.coverImage,
        },
        {
          key: 'twitter:title',
          name: 'twitter:title',
          content: this.$page.blog.title,
        },
        {
          key: 'twitter:description',
          name: 'twitter:description',
          content: this.$page.blog.description,
        },
        {
          key: 'twitter:image',
          name: 'twitter:image',
          content: 'https://www.yellowbrick.com' + this.$page.blog.coverImage,
        },
        {
          key: 'twitter:url',
          name: 'twitter:url',
          content: 'https://www.yellowbrick.com' + this.$page.blog.path,
        }
      ]
    }
  }
}
</script>

<page-query>
  query Blog($id: ID!) {
    blog(id: $id) {
      title
      description
      author
      content
      coverImage
      date(format: "MMMM D, YYYY")
      categories {
        id
        title
        path
      }
    }
  }
</page-query>