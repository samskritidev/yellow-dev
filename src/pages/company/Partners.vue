<style scoped>
  .hero {
    background-image: url(/uploads/images/generic-bg.svg);
    background-size: cover;
    background-position: center;
  }

  .asterisk {
    @apply text-red-800;
  }

  :target {
    scroll-margin-top: 90px;
  }

  .hs-form-dark .hs-form-wrapper .form-columns-2 .hs-form-field {
    display: inline-block;
  }
</style>

<template>
  <Layout>
    <section class="hero flex flex-col bg-gray-700 py-24 px-6 xl:px-0">
      <div class="max-w-1200 w-full mx-auto text-white z-10">
        <h1 class="">Partners</h1>
        <p class="rfs-text-xl w-full md:w-1/2">Yellowbrick Data works with leading data management, data integration, and BI partners to unleash the power of your data with faster
          analytics.</p>
        <button v-scroll-to="`#solution`" class="button yellow mr-4 mb-4">Solution Partners</button>
        <button v-scroll-to="`#technology`" class="button yellow mr-4 mb-4">Technology Partners</button>
        <button v-scroll-to="`#become`" class="button yellow mr-4 mb-4" @click="expanded = !expanded">Become a Partner</button>
        <a href="https://yellowbrick.channeltivity.com/">
          <button class="button yellow">Partner Portal</button>
        </a>
      </div>
    </section>

    <section class="bg-white py-12 md:py-20 px-6 xl:px-0" id="solution">
      <div class="w-full max-w-1200 mx-auto">
        <h2>Solution Partners</h2>
      </div>
      <section class="flex flex-row flex-wrap py-16 max-w-1200 w-full mx-auto">
        <div v-for="solutionPartner in $page.partnerPage.solutionPartners" class="zoomer w-full sm:w-1/2 lg:w-1/3 xl:w-1/4">
          <div class="p-2 h-full">
            <a v-if="solutionPartner.url" :href="solutionPartner.url" target="_blank" class="bg-gray-700 h-full flex p-5 xs:p-8 md:p-10 relative">
              <img v-if="solutionPartner.photo" :src="solutionPartner.photo" class="w-full flex self-center" :alt="solutionPartner.name" />
              <div class="hvr-reveal flex">
                <div v-html="solutionPartner.body" class="flex text-lg leading-tight self-center" />
              </div>
            </a>
          </div>
        </div>
      </section>
    </section>

    <section class="bg-gray-100 py-12 md:py-20 px-6 xl:px-0" id="technology">
      <div class="w-full max-w-1200 mx-auto">
        <h2>Technology Partners</h2>
      </div>
      <section class="flex flex-row flex-wrap py-16 max-w-1200 w-full mx-auto">
        <div v-for="techPartner in $page.partnerPage.techPartners" class="zoomer w-full sm:w-1/2 lg:w-1/3 xl:w-1/4">
          <div class="p-2 h-full">
            <a v-if="techPartner.url" :href="techPartner.url" target="_blank" class="bg-gray-700 h-full flex p-5 xs:p-8 md:p-10 relative">
              <img v-if="techPartner.photo" :src="techPartner.photo" class="w-full flex self-center" :alt="techPartner.name" />
              <div class="hvr-reveal flex">
                <div v-html="techPartner.body" class="flex text-lg leading-tight self-center" />
              </div>
            </a>
          </div>
        </div>
      </section>
    </section>

    <section class="bg-gray-600 text-white py-12 md:py-20 px-6 xl:px-0" id="become">
      <div class="w-full max-w-1200 mx-auto" id="form-start">
        <h2 class="accent-heading">Become a Partner</h2>
        <p class="w-full md:w-1/2">Yellowbrick is growing rapidly, as is our partner ecosystem. We're looking for valuable partners that can enhance our offering and provide a customer-focused vision. Sign up below to get started.</p>

        <transition-expand>
          <div v-show="expanded" class="hs-form-light hs-form-inline bg-gray-100 text-gray-500 p-8 mb-8">
            <BaseHubspot :id="'007fec31-69e0-4022-99bc-bc8643a848e0'" :sfid="'7011G000000kg9oQAA'" />
          </div>
        </transition-expand>
        <button v-scroll-to="`#form-start`" @click="expanded = !expanded" class="button yellow">{{ expanded ? `Close Form` : `Get Started` }}</button>
      </div>
    </section>

  </Layout>
</template>

<script>
  import TransitionExpand from '~/components/TransitionExpand.vue'

  export default {
    components: {
      TransitionExpand
    },
    metaInfo: {
      title: 'Yellowbrick Partners',
      meta: [{
        key: 'description',
        name: 'description',
        content: 'Discover the amazing partnerships we have developed here at Yellowbrick or join us and see why so many are partnering with us.'
      }]
    },
    data() {
      return {
        expanded: false,
        formData: {}
      }
    },
    methods: {
      encode(data) {
        return Object.keys(data)
          .map(key => encodeURIComponent(key) + '=' + encodeURIComponent(data[key]))
          .join('&')
      },
      handleSubmit(e) {
        fetch('/thank-you/', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/x-www-form-urlencoded'
            },
            body: this.encode({
              'form-name': e.target.getAttribute('name'),
              ...this.formData,
            }),
          })
          .then(() => this.$router.push('/thank-you/'))
          .catch(error => alert(error))
      }
    }
  }
</script>


<page-query>
  query Page {
  partnerPage: pages(path: "/data/pages/partners") {
  solutionPartners {
  name
  url
  photo
  body
  categories
  }
  techPartners {
  name
  url
  photo
  body
  categories
  }
  }
  }
</page-query>