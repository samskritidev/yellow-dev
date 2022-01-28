<style scoped>
  .overline {
    border-top: 5px solid #FFCD32;
    font-weight: 600;
  }

  .main-box {
    padding: 17.334% 50px;
    display: block;
    width: 100%;
    height: 100%;

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
</style>

<template>
  <Layout>

    <section class="bg-gray-light pt-12 px-6 xl:px-0">
      <div class="flex flex-col max-w-1200 w-full mx-auto">
        <ul class="m-0 py-8">
          <li class="accent-yellow">
            <g-link to="/blog/">All Posts</g-link>
          </li>
          <li class="accent-yellow" v-for="category in this.categories" :key="category.id" :class="{ 'active': $page.category.title === category.title }">
            <g-link :to="category.path"> {{ category.title }} </g-link>
          </li>
        </ul>
      </div>
    </section>

    <section class="bg-gray-light px-6 xl:px-0">
      <div class="max-w-1200 w-full mx-auto py-8">
        <div class="flex flex-row flex-wrap -mx-6">
          <g-link :to="edge.node.path" v-for="edge in $page.category.belongsTo.edges" :key="edge.node.id" class="flex flex-col w-full md:w-1/2 relative current-post p-6">
            <div class="flex flex-col w-full h-full" :style="`background-image: url('${edge.node.coverImage}'); background-size: cover; background-position: right center`">
              <div class="p-10 md:px-6 w-full md:w-3/4 lg:w-7/12">
                <span class="block text-gray-200" v-text="edge.node.date" />
                <h4 class="rfs-text-xl text-white leading-none" v-html="edge.node.title" />
                <div class="arrow-only-white">Read Post</div>
              </div>
            </div>
          </g-link>
        </div>
      </div>
    </section>
  </Layout>
</template>

<script>
  export default {
    mounted() {
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
    },
    data: () => ({
      categories: []
    }),
    metaInfo() {
      return {
        title: this.$page.category.title,
        meta: [{
          key: 'description',
          name: 'description',
          content: 'Find blogs related to this Topic.'
        }]
      }
    }
  }
</script>

<page-query>
  query Category($id: ID!) {
  category(id: $id) {
  title
  path
  belongsTo {
  edges {
  node {
  ...on Blog {
  id
  title
  date(format: "DD MMM YYYY")
  path
  coverImage
  }
  }
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