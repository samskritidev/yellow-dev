<style scoped>
    .nav-arrow:after,.nav-arrow:before {
        --bg-opacity: 1;
        background-color: black;
    }
    .bg-blackish {
        background-color: rgba(13, 23, 28, .97);
    }
    #topnav {
        border-bottom: 1px solid black;
    }
    @media only screen and (max-width: 768px) {
        .mobile-menu {
            -webkit-overflow-scrolling: touch;
            overflow-y: scroll;
        }
    }
    #search-box {
        padding-left: 50px;
        padding-right: 50px;
    }
    @media(min-width: 880px) {
        .menu-item:hover > label > .submenu {
            display: block !important;
        }

        .submenu {
            margin: 0;
        }
    }

    .search-icon {
        height: 15px;
        width: auto;
    }

    .child {
        @apply ml-4;
    }
</style>


<template>
    <div>
        <header id="topnav" class="fixed flex flex-row cc:flex-col z-50 items-center w-full bg-white">
            <nav role="navigation" class="flex flex-col items-center space-between max-w-1400 mx-auto w-full px-5 py-3 cc:py-0">

                <div class="flex items-center w-full space-between">

                    <div role="navigation" class="text-white z-30 w-full flex flex-wrap justify-end xl:flex-no-wrap">
                        <a href="/" class="mr-auto flex-auto self-start py-4" >
                            <img  alt="Yellowbrick Blog Page" src="/uploads/logo.png" />
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

                            <li  class="flex relative text-black trans-bg-color pl-0 text-base hover:text-yellow1 menu-item cc:px-3 lg:px-6">
                                <label aria-haspopup="true" class="w-full relative">
                                    <div class="flex flex-row items-center">
                                        <span class="flex items-center cursor-pointer p-2 pl-6 cc:px-2 cc:py-2">Categories</span>
                                        <span class="nav-arrow text-black" />
                                    </div>
                                    <transition name="slider">
                                        <ul  style="display:none;" class="cc:absolute py-3 whitespace-no-wrap bg-yellow1 cc:mt-4 min-w-full cc:min-w-200 rounded-sm submenu" aria-label="submenu">
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
                                <span style="transform: rotate(-45deg);" class="inline-block cursor-pointer pb-2" @click="searchClick"><img src="~@/assets/images/icons/search-icon.svg" class="search-icon" /></span>
                                <transition name="pusher">
                                    <search-blog v-show="searchFocus" v-model="searchResults"  style="top:3px;right:28px;z-index:60;" />
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

        <slot />

        <footer>
            <section class="bg-gray-500 px-5">
                <div class="max-w-1400 mx-auto py-12 md:py20 px-6 lg:px-0">
                    <div class="w-full flex flex-row items-center mb-12">
                        <g-link to="/">
                            <svg xmlns="http://www.w3.org/2000/svg" x="0" y="0" viewBox="0 0 242.7 40.9" xml:space="preserve" style="width:200px;max-width:200px;">
                            <path fill="#f3f6f6" d="M186.5 15.4h3.4v2.8h.1c.2-.5.5-.9.9-1.3s.8-.7 1.3-1 1-.5 1.5-.7c.6-.2 1.1-.2 1.7-.2s1.1.1 1.5.2l-.2 3.7c-.3-.1-.6-.1-.8-.2-.3-.1-.6-.1-.8-.1-1.7 0-3 .5-3.8 1.4-.9.9-1.3 2.4-1.3 4.4v9h-3.4v-18h-.1zM66.2 18L58.6 7.6h-4.4l10.4 13.6v12.2h3.5V21L78.3 7.6h-4.4L66.2 18zM130.9 24.4c0 5.2-4.2 9.5-9.5 9.5s-9.5-4.2-9.5-9.5c0-5.2 4.2-9.5 9.5-9.5s9.5 4.3 9.5 9.5zm-9.4-6.1c-3.4 0-6.1 2.7-6.1 6.1s2.7 6.1 6.1 6.1 6.1-2.7 6.1-6.1-2.8-6.1-6.1-6.1zM82.5 14.9c-5.2 0-9.5 4.2-9.5 9.5s4.2 9.5 9.5 9.5c2.8 0 5.3-1.2 7-3.1l-3-1.7c-1.1.9-2.5 1.5-4 1.5-2.9 0-5.4-2.1-6-4.8h15.3c.1-.4.1-.8.1-1.3 0-5.3-4.2-9.6-9.4-9.6zm0 3.4c2.8 0 5.2 2 5.9 4.6H76.6c.6-2.6 3-4.6 5.9-4.6zM216.6 30.5c-3.4 0-6.1-2.7-6.1-6.1s2.7-6.1 6.1-6.1c1.5 0 2.9.6 4 1.5l3-1.7c-1.7-1.9-4.2-3.2-7-3.2-5.2 0-9.5 4.2-9.5 9.5s4.2 9.5 9.5 9.5c2.8 0 5.3-1.2 7-3.1l-3-1.7c-1.1.8-2.5 1.4-4 1.4zM132.3 15.4h3.8l4 13.5h.1l4.3-13.5h3.6l4.6 13.5h.1l3.8-13.5h3.6l-5.8 18h-3.5l-4.8-13.5h-.1l-4.4 13.5H138l-5.7-18zM199.8 15.4h3.4v18h-3.4v-18zM199.8 8.9h3.4v3.4h-3.4V8.9zM95.8 33.4h3.4V9.6l-3.4-2v25.8zM104.8 33.4h3.4V9.6l-3.4-2v25.8zM173.2 14.9c-2.3 0-4.4.8-6.1 2.2V9.5l-3.4-2v25.8h3.4v-1.8c1.6 1.4 3.8 2.2 6.1 2.2 5.2 0 9.5-4.2 9.5-9.5 0-5-4.3-9.3-9.5-9.3zm0 15.6c-3.4 0-6.1-2.7-6.1-6.1s2.7-6.1 6.1-6.1 6.1 2.7 6.1 6.1-2.7 6.1-6.1 6.1zM233.6 23.6l8.4-8.2h-4.7l-7.8 7.8V9.6l-3.4-2v25.8h3.4v-9.3l8.4 9.3h4.8l-9.1-9.8z" />
                            <path fill="#fdcf41" d="M35.4 0H18.7l-1.8 3.2 8.3 14.5h16.7l1.9-3.2L35.4 0z" />
                            <path fill="#cf8a00" d="M35.4 0l-1.8 3.2 8.3 14.5 1.9-3.2L35.4 0z" />
                            <path fill="#fff3a2" d="M35.4 0l-1.8 3.2H16.9L18.7 0h16.7z" />
                            <path fill="#fdcf41" d="M0 20.5L8.3 35H12l8.4-14.5L12 6H8.3L0 20.5z" />
                            <path fill="#fff3a2" d="M0 20.5h3.7L12 6H8.3L0 20.5z" />
                            <path fill="#cf8a00" d="M0 20.5h3.7L12 35H8.3L0 20.5z" />
                            <path fill="#fdcf41" d="M35.4 40.9l8.4-14.4-1.9-3.2H25.2l-8.3 14.5 1.8 3.1h16.7z" />
                            <path fill="#cf8a00" d="M35.4 40.9l-1.8-3.1H16.9l1.8 3.1h16.7z" />
                            <path fill="#cf8a00" d="M35.4 40.9l-1.8-3.1 8.3-14.5 1.9 3.2-8.4 14.4z" /></svg>
                        </g-link>
                    </div>
                    <div class="flex flex-row flex-wrap">
                        <div class="flex flex-wrap w-full lg:w-1/2 mb-10">

                            <div class="w-full sm:w-1/2 flex flex-col">
                                <ul class="list-none p-0 m-0 text-gray-200 leading-loose">
                                    <li><g-link to="/products/data-warehouse/">Products</g-link></li>
                                    <li><g-link to="/customers/">Customers</g-link></li>
                                    <li><g-link to="/resources/">Resource Library</g-link></li>
                                    <li><g-link to="/company/partners/">Partners</g-link></li>
                                    <li><g-link to="/company#teammembers">Team</g-link></li>
                                    <li><g-link to="https://support.yellowbrick.io/">Customer Center</g-link></li>
                                </ul>
                            </div>

                            <div class="w-full sm:w-1/2 flex flex-col">
                                <ul class="list-none p-0 m-0 text-gray-200 leading-loose">
                                    <li>
                                        <g-link to="/contact-us/">Contact Us</g-link>
                                    </li>
                                    <li>
                                        <g-link to="/company/careers/">Careers</g-link>
                                    </li>
                                    <li>
                                        <g-link to="/resources/webcasts/">Virtual Events</g-link>
                                    </li>
                                    <li>
                                        <g-link to="/blog/">Blog</g-link>
                                    </li>
                                    <li>
                                        <g-link to="/newsroom/">News</g-link>
                                    </li>
                                    <li>
                                        <g-link to="/company/">Company</g-link>
                                    </li>
                                    <li>
                                        <g-link to="/terms/">Terms & Privacy Policy</g-link>
                                    </li>
                                </ul>
                            </div>
                        </div>

                        <div class="flex flex-wrap w-full lg:w-1/2">
                            <div class="w-full sm:w-1/2 flex flex-col pb-8 sm:pb-0">
                                <p class="text-gray-200">
                                    <span class="text-white font-semibold">US</span><br />
                                    Phone 877.492.3282<br />
                                    <a class="text-yellow1" href="mailto:info@yellowbrick.com">info@yellowbrick.com</a>
                                </p>


                                <p class="text-gray-200">
                                    <span class="text-white font-semibold">US Headquarters</span><br />
                                    660 W. Dana Street<br />
                                    Mountain View, CA  94041
                                </p>

                            </div>

                            <div class="w-full sm:w-1/2 flex flex-col">
                                <p class="text-gray-200">
                                    <span class="text-white font-semibold">International</span><br />
                                    Phone +1.650.687.0896<br />
                                    <a class="text-yellow1" href="mailto:info@yellowbrick.com">info@yellowbrick.com</a>
                                </p>


                                <p class="text-gray-200">
                                    <span class="text-white font-semibold">Europe Headquarters</span><br />
                                    32 London Bridge Street, TOG 24/25<br />
                                    London, SE1 9SG UK
                                </p>
                                <p class="text-gray-200">
                                    <span class="text-white font-semibold">Asia Headquarters</span><br />
                                    13th Floor, 2 Blenheim Ave<br />
                                    Tsin Sha Tsui, Hong Kong
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
            </section>
            <section class="py-4 bg-gray-500 text-gray-100 px-5">
                <div class="max-w-1400 mx-auto flex flex-row flex-wrap justify-between items-center">
                    <p class="flex flex-col w-full sm:w-3/4 text-sm text-center sm:text-left mb-6 sm:mb-0">
                        &copy; {{new Date().getFullYear()}} Yellowbrick Data, Inc. All rights reserved.
                    </p>

                    <div class="flex w-full sm:w-1/4 justify-center sm:justify-end">
                        <a href="https://twitter.com/yellowbrickdata" class="icon mr-6" aria-label="Yellowbrick Twitter Page">
                            <svg class="sm-icons twitter w-4 md:w-6 h-4 md:h-6" data-name="twitter" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 128 128">
                                <path d="M127.85 35.26a52.47 52.47 0 01-15 4.12 26.25 26.25 0 0011.49-14.47 52.37 52.37 0 01-16.6 6.35A26.16 26.16 0 0063.18 55.1 74.24 74.24 0 019.29 27.79a26.17 26.17 0 008.09 34.9 25.91 25.91 0 01-11.84-3.27v.33a26.17 26.17 0 0021 25.64 26.15 26.15 0 01-6.89.91 26.56 26.56 0 01-4.92-.46A26.17 26.17 0 0039.12 104a52.42 52.42 0 01-32.47 11.2 53.62 53.62 0 01-6.24-.37 74 74 0 0040.08 11.75c48.09 0 74.39-39.84 74.39-74.39 0-1.14 0-2.26-.07-3.39a52.92 52.92 0 0013.04-13.54z" />
                            </svg>
                        </a>

                        <a href="https://www.linkedin.com/company/yellowbrickdata/" class="icon" aria-label="Yellowbrick Linkedin Page">
                            <svg class="sm-icons linkedin w-4 md:w-6 h-4 md:h-6" data-name="linkedin" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 128 128">
                                <defs></defs>
                                <path d="M2.42 42.32h26.49v85.12H2.42zM15.67 0A15.35 15.35 0 11.32 15.34 15.34 15.34 0 0115.67 0M45.5 42.32h25.37V54h.36c3.53-6.69 12.16-13.75 25-13.75C123.05 40.2 128 57.83 128 80.76v46.68h-26.45V86.05c0-9.87-.17-22.57-13.75-22.57-13.8 0-15.87 10.75-15.87 21.86v42.1H45.5z" />
                            </svg>
                        </a>
                    </div>
                </div>
            </section>
        </footer>
    </div>
</template>

<script>import {
    disableBodyScroll,
    clearAllBodyScrollLocks
  } from 'body-scroll-lock'
    import SearchBlog from '@/components/SearchBlog'


  export default {
    components: {
          SearchBlog
    },
        data: () => ({
            categories: [],
            searchResults: null,
      menu: [
        {
          label: 'Industries',
          show: false,
          subitems: [{
              label: 'Data Lake Augmentation',
              route: '/solutions/data-lake-augmentation/'
            },
            {
              label: 'Data Warehouse Modernization',
              route: '/solutions/data-warehouse-modernization/',
              parent: true
            },
          ]
        },
        {
          label: 'News',
            route: '/News/'
        },
        {
          label: 'More',
          show: false,
          subitems: [{
              label: 'Solution Partners',
              route: '/company/partners/#solution'
            },
          ]
        },
      ],
      showDrawer: false,
      searchFocus: false,
      openNav: false,
    }),
    beforeCreate(){

  },
    mounted() {
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
      // temp code to remove old service workers
      self.addEventListener('install', function(e) {
        self.skipWaiting();
      });

      self.addEventListener('activate', function(e) {
        self.registration.unregister()
          .then(function() {
            return self.clients.matchAll();
          })
          .then(function(clients) {
            clients.forEach(client => client.navigate(client.url))
          });
      });

      clearAllBodyScrollLocks()
      document.addEventListener('click', this.clickAnywhere)
      document.addEventListener('keydown', this.pressAnything)
      document.addEventListener('scroll', this.scrollAnytime)

      setTimeout(function(document){
        if(!document)
          return;
        const path = 'https://www.yellowbrick.com' + document.location.pathname;
        document.head.querySelector('meta[name="og:url"]').content = path;
        document.head.querySelector('meta[name="twitter:url"]').content = path;
      }(document))
    },
    beforeDestroy() {
      document.removeEventListener('click', this.clickAnywhere)
      document.removeEventListener('keydown', this.pressAnything)
      document.removeEventListener('scroll', this.scrollAnytime)
    },
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
        this.menu.forEach((item, x) => {
          if (!document.getElementById(`menu-${x}`).contains(e.target) && item.show) item.show = false
        })
        if (!document.getElementById('search-box').contains(e.target)) this.searchFocus = false
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
    }
  }</script>
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