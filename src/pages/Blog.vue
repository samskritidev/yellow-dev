<style scoped>
    .rfs-text-4xl {
        margin-top: 20px;
        margin-bottom: 20px;
    }

    .active.pagerLink {
        background-color: #ffcd32;
        border: 1px solid black;
        font-weight: bold;
        font-size: 25px;
    }

    .nav-arrow {
        margin-right: -5px;
    }

    .pagerLink {
        font-weight: bold;
        color: black;
        font-size: 25px;
    }

    .featured-author {
        margin-bottom: 0.5rem;
    }

    .main-box {
        padding-top: 30%;
        &:hover

    {
        & .arrow-only

    {
        @apply text-teal;
        &:after

    {
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
        &:after

    {
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
        &:after

    {
        transform: translateX(10px);
        cursor: pointer;
        color: teal;
    }

    }
    }

    .current-post {
        & .arrow-only-white

    {
        @apply flex flex-row relative items-baseline rfs-text-base font-normal text-white;
        transition: all .2s ease;
        &:after

    {
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
        & .arrow-only-white

    {
        @apply text-teal;
        &:after

    {
        transform: translateX(10px);
        cursor: pointer;
        color: teal;
    }

    }
    }
    }

    .float-box {
        @apply absolute p-5;
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

        <header id="topnav" class="fixed flex flex-row cc:flex-col z-50 items-center w-full bg-white">
            <nav role="navigation" class="flex flex-col items-center space-between max-w-1400 mx-auto w-full px-5 py-3 cc:py-0">

                <div class="flex items-center w-full space-between">

                    <div role="navigation" class="text-white z-30 w-full flex flex-wrap justify-end xl:flex-no-wrap">
                        <a href="/" class="mr-auto flex-auto self-start py-4">
                            <img alt="Yellowbrick Blog Page" src="/uploads/logo.png" />
                        </a>

                        <div :class="[showDrawer ? 'bg-transparent-75' : 'hidden']" class="fixed cc:hidden z-40 inset-0 trans-bg-color" @click="toggleDrawer(false)" />
                        <ul ref="drawer" :style="{ right: showDrawer ? '0px' : '-100%' }" style="transition: right 0.25s ease;" class="fixed z-100 cc:static cc:flex items-center inset-y-0 h-screen cc:h-auto bg-black cc:bg-transparent w-full cc:w-auto m-0 mobile-menu">
                            <li class="cc:hidden flex justify-between p-2">
                                <g-link to="/" class="p-2 pl-4">
                                    <img alt="Yellowbrick Data Logo" src="/uploads/images/yb-logo-dark.svg" width="130" />
                                </g-link>
                                <div :class="{ hidden: !showDrawer }" class="p-2" @click="toggleDrawer(false)">
                                    <button id="close"></button>
                                </div>
                            </li>

                            <li class="flex relative text-black trans-bg-color pl-0 text-base hover:text-yellow1 menu-item cc:px-3 lg:px-6">
                                <label aria-haspopup="true" class="w-full relative">
                                    <div class="flex flex-row items-center">
                                        <span class="flex items-center cursor-pointer p-2 pl-6 cc:px-2 cc:py-2">Categories</span>
                                        <span class="nav-arrow text-black" />
                                    </div>
                                    <transition name="slider">
                                        <ul style="display:none;" class="cc:absolute py-3 whitespace-no-wrap bg-yellow1 cc:mt-4 min-w-full cc:min-w-200 rounded-sm submenu" aria-label="submenu">
                                            <li class="main-nav-link" v-for="category in this.categories" :key="category.id">
                                                <g-link :to="category.path" aria-haspopup="true" class="flex px-8 py-2 cc:px-2 w-full"> {{ category.title }} </g-link>
                                            </li>
                                        </ul>
                                    </transition>
                                </label>
                            </li>


                            <li v-for="(item, x) in menu" :key="x" :id="`menu-${x}`" class="flex cc:px-3 lg:px-6 relative text-black trans-bg-color pl-0 text-base hover:text-yellow1 menu-item" :class="{'cc:pl-3 lg:pl-6' : x === 0, 'cc:pl-3 lg:pl-6' : x === Object.keys(menu).length - 2, 'cc:pl-3 lg:pl-6' : x !== 0 && x !== Object.keys(menu).length - 2}"
                                @click="item.show = !item.show">
                                <g-link v-if="item.route" :to="item.route" class="p-2 px-6 cc:px-2 cc:py-2">{{ item.label }}</g-link>
                                <label v-else aria-haspopup="true" class="w-full relative">
                                    <div class="flex flex-row items-center">
                                        <span v-text="item.label" class="flex items-center cursor-pointer p-2 pl-6 cc:px-2 cc:py-2" />
                                        <span class="nav-arrow text-black" />
                                    </div>
                                    <transition name="slider">
                                        <ul v-show="item.show" class="cc:absolute py-3 whitespace-no-wrap bg-yellow1 cc:mt-4 min-w-full cc:min-w-200 rounded-sm submenu" aria-label="submenu">
                                            <li v-for="(subitem, y) in item.subitems" :key="y" class="main-nav-link" :class="{'child' : subitem.indent, 'parent' : subitem.parent}">
                                                <g-link :to="subitem.route" aria-haspopup="true" class="flex px-8 py-2 cc:px-2 w-full">{{ subitem.label }}</g-link>
                                            </li>
                                        </ul>
                                    </transition>
                                </label>
                            </li>
                            <li id="search-box" class="flex list-none font-normal rfs-text-lg p-1 pl-6 cc:px-2 cc:py-1 relative">
                                <span style="transform: rotate(-45deg);" class="inline-block cursor-pointer pb-2" @click="searchClick"><img src="/uploads/icons/search-icon.svg" class="search-icon" /></span>
                                <transition name="pusher">
                                    <search-blog v-show="searchFocus" v-model="searchResults" class="cc:absolute text-transparent" style="top:3px;right:28px;z-index:60;" />
                                </transition>
                            </li>
                        </ul>

                    </div>
                    <div class="cursor-pointer cc:hidden flex-1 flex items-center justify-end ml-8" @click="toggleDrawer(true)">
                        <button id="hamburger" aria-label="Show the menu" />
                    </div>

                </div>
            </nav>
        </header>
        <section class="flex flex-col pb-2 pt-32 px-6 xl:px-0 bg-white">
        </section>
        <section class="px-6 xl:px-0 bg-white pb-16" v-if="featuredBlog" style="border-bottom: 1px solid #0000002e;">
            <div class="flex flex-col md:flex-row max-w-1200 w-full mx-auto relative">

                <div class="w-full md:w-1/2 main-box relative">
                    <div class="float-box">
                        <img :src="`${featuredBlog.coverImage}`" />
                    </div>
                </div>
                <div class="w-full md:w-1/2 main-box relative">
                    <div class="float-box text-black">
                        <template v-if="featuredBlog.categories">
                            <a v-for="(category) in featuredBlog.categories" :key="category.id" v-text="category.title === 'yellowbrick and tpc-ds' ? 'Yellowbrick and TPC-DS' : category.title" :href="`/blog/category/${category.title}`" class="uppercase font-bold text-yellow1 leading-none mr-2 inline" />
                        </template>
                        <g-link :to="featuredBlog.path"><h2 class="rfs-text-4xl font-bold" style="line-height: 1.1;" v-html="featuredBlog.title" /></g-link>

                        <p class="rfs-text-base leading-tight" v-html="featuredBlog.description" />
                        <div class="flex flex-col md:flex-row md:w-1/2">
                            <div class="w-full md:w-1/4" style="margin-right:20px">
                                <img src="/uploads/author.png" />
                            </div>
                            <div class="w-full md:w-2/3">
                                <p class="featured-author font-bold" v-text="featuredBlog.author" />
                                <p v-text="featuredBlog.date" />
                            </div>
                        </div>
                    </div>
                </div>
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

        <section class="px-6 xl:px-0 py-12" id="current_post">
            <div class="max-w-1200 w-full mx-auto">
                <h1 class="text-yellow1 uppercase font-bold">Current Posts</h1>
                <div class="flex flex-row flex-wrap -mx-6">
                    <div v-for="edge in searchResults ? searchResults : $page.allBlog.edges" :key="edge.node.id" class="flex flex-col w-full relative current-post p-6">
                        <div class="flex flex-col md:flex-row max-w-1200 w-full mx-auto relative">
                            <div :to="featuredBlog.path" class="w-full md:w-1/3 main-box relative">
                                <div class="float-box text-white">
                                    <img :src="`${edge.node.authorImage}`" />
                                </div>
                            </div>
                            <div class="w-full md:w-2/3 main-box relative">
                                <div class="float-box text-black">
                                    <!-- <h6 class="text-yellow2 hidden md:block">Data Warehouse Modernization</h6> -->
                                    <template v-if="edge.node.categories">
                                        <a v-for="(category) in edge.node.categories" :key="category.id" v-text="category.title === 'yellowbrick and tpc-ds' ? 'Yellowbrick and TPC-DS' : category.title" :href="`/blog/category/${category.title}`" class="uppercase font-bold text-yellow1 leading-none mr-2 inline" />
                                    </template>
                                    <g-link :to="edge.node.path"><h4 class="rfs-text-4xl text-black font-bold" v-html="edge.node.title" /></g-link>
                                    <h4 class="rfs-text-base text-black" v-html="edge.node.description" />
                                    <div class="flex flex-col md:flex-row md:w-1/2">
                                        <div class="w-full md:w-1/4" style="margin-right:20px">
                                            <img src="/uploads/author.png" />
                                        </div>
                                        <div class="w-full md:w-2/3">
                                            <p class="featured-author font-bold" v-text="edge.node.author" />
                                            <p v-text="edge.node.date" />
                                        </div>
                                    </div>
                                </div>
                            </div>

                            <!-- <img src="/uploads/blog/abstract4.jpg" alt="abstract" class="self-start" /> -->

                        </div>
                    </div>
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

        <Pager v-if="!searchResults" class="flex w-full mx-auto py-8 bg-white text-3xl justify-center" :info="$page.allBlog.pageInfo" linkClass="pagerLink" />

    </Layout>
</template>

<script>
    import Layout from '~/layouts/Blog.vue'
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
            Layout,
            Pager,
            SearchBlog,
            BiWeeklyBanner
        },
        data: () => ({
            searchResults: null,
            featuredBlog: null,
            categories: [],
            menu: [
        {
          label: 'Industries',
          show: false,
              subitems: [
                  {
                      label: 'Financial Services',
                      route: '/solutions/financial-services/',
                      indent: true
                  },
                  {
                      label: 'Healthcare & Life Sciences',
                      route: '/solutions/healthcare-life-sciences/',
                      indent: true
                  },
                  {
                      label: 'Insurance',
                      route: '/solutions/insurance/',
                      indent: true
                  },
                  {
                      label: 'Retail',
                      route: '/solutions/retail/',
                      indent: true
                  },
                  {
                      label: 'Federal',
                      route: '/solutions/federal/',
                      indent: true
                  },
                  {
                      label: 'Telecommunications',
                      route: '/solutions/telecom/',
                      indent: true
                  },
          ]
        },
        {
          label: 'News',
            route: '/newsroom/'
        },
        {
          label: 'More',
          show: false,
          subitems: [{
              label: 'Coming Soon',
              route: '#'
            },
          ]
        },
      ],
      showDrawer: false,
      searchFocus: false,
      openNav: false,
        }),
        methods: {
            toggleDrawer(open) {
                this.showDrawer = open
                if (open) disableBodyScroll(this.$refs.drawer)
                else clearAllBodyScrollLocks()
            },
            searchClick() {
                this.searchFocus = true
                this.$nextTick(() => {
                    document.getElementById('search-box').focus()
                })
            },
            clickAnywhere(e) {
                var ignoreClickOnMeElement = document.getElementById('search-box');
                var isClickInsideElement = ignoreClickOnMeElement.contains(e.target);
                if (!isClickInsideElement) {
                    document.getElementById("search_div").style.display = "none";
                }
                else {
                    document.getElementById("search_div").style.display = "block";
                }
            },
            pressAnything(e) {
                if (e.key === 'Escape') {
                    this.showDrawer = false
                    this.searchFocus = false
                    this.menu.forEach((item, x) => {
                        if (item.show) item.show = false
                    })
                }
            }
        },
        mounted() {
            document.addEventListener('click', this.clickAnywhere)
            document.addEventListener('keydown', this.pressAnything)
            document.addEventListener('scroll', this.scrollAnytime)
            if (this.$page?.featuredBlog?.edges?.length > 0) {
                this.featuredBlog = this.$page.featuredBlog.edges[0].node;
            }
            if (this.$page?.allCategory?.edges?.length > 0) {
                this.$page.allCategory.edges.forEach((category) => {
                    this.categories.push(category.node);
                })
                this.categories.sort(function (a, b) {
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
    author
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
    author
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
    author
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