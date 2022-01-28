<style scoped>
  .main-box {
    padding-top: 50%;

    &:hover {
      & .arrow-only {
        @apply text-teal;

        &:after {
          transform: translateX(10px);
          cursor: pointer;
          color: teal;
        }
      }
    }
  }

  .pic {
    background-image: url(/uploads/blog/abstract1-square.jpg);
    background-size: cover;
    background-position: center;
  }

  .arrow-only {
    @apply flex flex-row relative items-baseline rfs-text-base font-normal;
    transition: all .2s ease;

    &:after {
      @apply flex ml-2;
      content: '';
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 48 30'%3E%3Cpath d='M47.2 13.2L34 .7c-1-1-2.6-.9-3.6.1s-.9 2.6.1 3.6l8.6 8.1H2.5C1.1 12.5 0 13.6 0 15s1.1 2.5 2.5 2.5h36.6l-8.6 8.1c-1 1-1.1 2.6-.1 3.6.5.5 1.2.8 1.8.8.6 0 1.3-.2 1.7-.7l13.2-12.5c.5-.5.8-1.1.8-1.8.1-.7-.2-1.4-.7-1.8z' fill='%231f292e'/%3E%3C/svg%3E ");
      width: 16px;
      height: 10px;
      transform: translateX(0);
      transition: all .2s ease;
    }

    &:hover {
      @apply text-teal;

      &:after {
        transform: translateX(10px);
        cursor: pointer;
        color: teal;
      }
    }
  }

  .current-post {
    & .arrow-only-white {
      @apply flex flex-row relative items-baseline rfs-text-base font-normal text-white;
      transition: all .2s ease;

      &:after {
        @apply flex ml-2;
        content: '';
        background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 48 30'%3E%3Cpath d='M47.2 13.2L34 .7c-1-1-2.6-.9-3.6.1s-.9 2.6.1 3.6l8.6 8.1H2.5C1.1 12.5 0 13.6 0 15s1.1 2.5 2.5 2.5h36.6l-8.6 8.1c-1 1-1.1 2.6-.1 3.6.5.5 1.2.8 1.8.8.6 0 1.3-.2 1.7-.7l13.2-12.5c.5-.5.8-1.1.8-1.8.1-.7-.2-1.4-.7-1.8z' fill='%231f292e'/%3E%3C/svg%3E ");
        filter: invert(1);
        width: 16px;
        height: 10px;
        transform: translateX(0);
        transition: all .2s ease;
      }
    }

    &:hover {
      & .arrow-only-white {
        @apply text-teal;

        &:after {
          transform: translateX(10px);
          cursor: pointer;
          color: teal;
        }
      }
    }
  }

  .float-box {
    @apply absolute p-10;
    top: 50%;
    transform: translateY(-50%);
  }

  @media only screen and (max-width: 640px) {
    .main-box {
      padding-top: 0%;
    }

    .float-box {
      @apply relative p-10;
      top: 0;
      left: 0;
      transform: translateY(0%);
    }
  }

  .bg-mask {
    @apply z-0 absolute top-0 bottom-0 left-0 right-0;
    background: rgba(0, 0, 0, .85);
  }

  .featured-date,
  .currentPost-date {
    font-size: 14px;
  }
</style>

<template>
  <Layout>
    <section class="flex flex-col pb-2 pt-32 px-6 xl:px-0 bg-gray-100">
      <div class="max-w-1200 w-full mx-auto z-10">
        <div class="flex flex-col md:flex-row w-full items-center">
          <h1 class="rfs-text-4xl w-full md:w-1/2 m-0 p-0 leading-none">Blog</h1>
          <div class="flex flex-col px-0 xl:px-0 z-10 w-full md:w-1/2">
            <search-blog v-model="searchResults" />
          </div>
        </div>
        <ul class="m-0 p-0 py-6">
          <li class="accent-dark" v-for="category in this.categories" :key="category.id">
            <g-link :to="category.path"> {{ category.title }} </g-link>
          </li>
        </ul>

      </div>
    </section>

    <section class="px-6 xl:px-0 bg-gray-100 pb-16" v-if="featuredBlog">
      <div class="flex flex-col md:flex-row max-w-1200 w-full mx-auto relative" :style="`background-image: url('${featuredBlog.coverImage}'); background-size: cover;`">
        <g-link :to="featuredBlog.path" class="w-full md:w-1/2 main-box relative">
          <div class="float-box text-white">
            <h6 class="uppercase text-yellow1 rfs-text-l">Featured Post</h6>
            <span class="featured-date" v-text="featuredBlog.date" />
            <h2 class="rfs-text-4xl" style="line-height: 1.1;" v-html="featuredBlog.title" />
            <p class="rfs-text-base leading-tight" v-html="featuredBlog.description" />
            <div class="">Read post</div>
          </div>
        </g-link>
        <div class="hidden sm:block md:w-1/2">
        </div>

      </div>
    </section>

    <!-- <section class="px-6 xl:px-0 py-12">
      <div class="max-w-1200 w-full mx-auto">
        <h3>Current Posts</h3>
        <div class="flex flex-col md:flex-row">
          <g-link :to="edge.node.path" v-for="edge in $page.latestBlogs.edges" :key="edge.node.id" class="flex flex-col w-full md:w-1/2 relative current-post" :style="`background-image: url('${edge.node.coverImage}'); background-size: cover;`">
            <div class="p-10 md:px-6 w-full md:w-3/4 lg:w-7/12">
              <span class="block text-gray-200" v-text="edge.node.date" />
              <h4 class="rfs-text-xl text-white leading-none" v-html="edge.node.title" />
              <div class="arrow-only-white">Read post</div>
            </div>
          </g-link>
        </div>
      </div>
    </section> -->

    <section class="px-6 xl:px-0 py-12">
      <div class="max-w-1200 w-full mx-auto">
        <h3>Current Posts</h3>
        <div class="flex flex-row flex-wrap -mx-6">
          <g-link :to="edge.node.path" v-for="edge in searchResults ? searchResults : $page.allBlog.edges" :key="edge.node.id" class="flex flex-col w-full md:w-1/2 relative current-post p-6">
            <div class="flex flex-col w-full h-full" :style="`background-image: url('${edge.node.coverImage}'); background-size: cover; background-position: right center`">
              <div class="p-10 md:px-6 w-full md:w-3/4 lg:w-7/12">

                <!-- <h6 class="text-yellow2 hidden md:block">Data Warehouse Modernization</h6> -->

                <span class="block text-gray-200 currentPost-date" v-text="edge.node.date" />
                <h4 class="rfs-text-xl text-white" v-html="edge.node.title" />
                <div class="arrow-only-white">Read post</div>
              </div>

              <!-- <img src="/uploads/blog/abstract4.jpg" alt="abstract" class="self-start" /> -->

            </div>
          </g-link>
        </div>
      </div>
    </section>

    <!-- <section class="px-6 xl:px-0">
      <div class="min-h-screen max-w-1200 w-full mx-auto">
        <h3>Previous Posts</h3>
        <div class="flex flex-wrap justify-start -mx-6">
          <div class="zoomer flex w-full sm:w-1/2 lg:w-1/3" v-for="edge in searchResults ? searchResults : $page.allBlog.edges" :key="edge.node.id">
            <div class="flex-col m-6 relative">
              <g-link :to="edge.node.path">
                <div class="text-sm font-normal self-end text-gray-700 py-1">{{ edge.node.date }}</div>
                <img v-if="edge.node.coverImage" :src="edge.node.coverImage" :alt="edge.node.title" />

                <img src="/uploads/blog/modernize.jpg" alt="abstract" class="" />

                <div class="self-end capitalize my-4 leading-none" v-if="edge.node.categories">
                  <span v-for="category in edge.node.categories" :key="category.id" v-text="category.title.replace('-', ' ')" class="text-gray-800 leading-none" />
                </div>
                <div class="">
                  <h6 class="">{{ edge.node.title }}</h6>

                  <div class="rfs-text-sm">{{ edge.node.description }}</div>

                </div>

              </g-link>
            </div>
          </div>
        </div>
      </div>
    </section> -->

    <Pager v-if="!searchResults" class="flex w-full mx-auto py-8 bg-gray-light text-3xl justify-center" :info="$page.allBlog.pageInfo" linkClass="pagerLink" />

  </Layout>
</template>

<script>
  import {
    Pager
  } from 'gridsome'
  import SearchBlog from '~/components/SearchBlog.vue'
  import BiWeeklyBanner from '~/components/BiWeeklyBanner.vue'

  export default {
    metaInfo: {
      title: 'Yellowbrick Data Warehouse Blog',
      meta: [{
        key: 'description',
        name: 'description',
        content: 'The Yellowbrick Data Blog is about all things data warehouse. Here you will find a variety of topics discussing the benefits of the modern hybrid cloud data warhouse.'
      }]
    },
    components: {
      Pager,
      SearchBlog,
      BiWeeklyBanner
    },
    data: () => ({
      searchResults: null,
      featuredBlog: null,
      categories: []
    }),
    mounted() {
      if (this.$page?.featuredBlog?.edges?.length > 0) {
        this.featuredBlog = this.$page.featuredBlog.edges[0].node;
      }
      if (this.$page?.allCategory?.edges?.length > 0) {
        this.$page.allCategory.edges.forEach((category) => {
          this.categories.push(category.node);
        })
        this.categories.sort(function(a, b) {
          let optA = a.title.toUpperCase();
          let optB = b.title.toUpperCase();
          return (optA < optB) ? -1 : (optA > optB) ? 1 : 0;
        });
      }
    }
  }
</script>

<page-query>
  query Blog($page: Int) {
  featuredBlog: allBlog(filter: { featured: { eq: true }}, limit: 1, sortBy: "date", order: DESC) {
  edges {
  node {
  id
  title
  description
  date(format: "MMMM D, YYYY")
  categories {
  id
  title
  }
  path
  coverImage
  }
  }
  }
  latestBlogs: allBlog(limit: 2, sortBy: "date", order: DESC) {
  edges {
  node {
  id
  title
  description
  date(format: "MMMM D, YYYY")
  categories {
  id
  title
  }
  path
  coverImage
  }
  }
  }
  allBlog(perPage: 12, page: $page, sortBy: "date", order: DESC) @paginate {
  pageInfo {
  totalPages
  currentPage
  isFirst
  isLast
  }
  edges {
  node {
  id
  title
  description
  date(format: "MMMM D, YYYY")
  categories {
  id
  title
  }
  path
  coverImage
  }
  }
  }
  allCategory {
  edges {
  node {
  id
  title
  path
  }
  }
  }
  }
</page-query>