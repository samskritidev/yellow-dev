<style scoped>
.hero {
  background-image: url(/uploads/images/hero-new.svg);
  background-size: cover;
  background-position: center center;
  &:after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    @apply bg-gray-700 absolute z-0;
    opacity: .7;
  }
}
.hero-half {
  @apply bg-white;
  &:after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 60%;
    background-image: url(/uploads/images/hero-new.svg);
    background-size: cover;
    background-position: center center;
    @apply bg-gray-700 absolute z-0;
  }
}

.predictability-bg {
  background-image: url(/uploads/images/predictability-bg.svg);
  background-position: bottom right;
  background-repeat: no-repeat;
  background-size: 50%;
}

.dk-bg {
	color: #ffffff !important;
}


.float-form {
	@apply relative p-8 bg-gray-200 shadow-lg;
}
</style>

<template>
  <Layout>
    <section class="hero flex bg-gray-700 py-10 md:py-12 text-white px-6 xl:px-0">
      <div class="flex flex-col md:flex-row max-w-1200 w-full py-8 mx-auto relative z-10">
          
					<div class="w-full md:w-2/3 p-0 md:pr-16 text-gray-700 md:text-white">
            <h5 class="text-yellow1 mb-6 md:mb-2">Featured eBook:</h5>
						<div class="bg-white md:bg-transparent p-6 md:p-0">
							<h1 class="p-0">Replacing Netezza</h1>
              <div class="float-none lg:float-right w-full xs:w-3/4 sm:mx-0 shadow-md sm:shadow-none lg:w-1/2 m-0 mb-8 lg:ml-10 lg:mb-12 lg:mt-3">
                <img src="/uploads/ebook-netezza.jpg" class="w-full" alt="Replace Netezza with Yellowbrick Data Warehouse" />
              </div>
							<p class="rfs-text-lg">Netezza was introduced in 2003 and enabled organizations to analyze more data, faster. Unfortunately, Netezza has not kept up with innovation and never made the leap to the cloud. Since IBM acquired Netezza, there has been inconsistency with their plans leaving many customers confused. </p>
              <p class="rfs-text-lg">Download this eBook if you are are looking for an easy, reliable way to upgrade to a high-performing system.</p>
              <h5 class="rfs-text-lg accent-heading mt-10 mb-0 pb-0">In this ebook you will learn:</h5>
              <div class="flex flex-col md:flex-row">
                <ul class="rfs-text-base w-full mb-0 pb-0 md:mb-2 md:pb-2">
                  <li>The pain points and critical problems Netezza users face</li>
                  <li>Why Yellowbrick is the clear replacement for Netezza</li>
                </ul>
                <ul class="rfs-text-base w-full pt-0 mt-0 md:mt-2 md:pt-2">
                  <li>How a Top 3 mobile company transformed its business with the upgrade to Yellowbrick </li>
                </ul>
              </div>
						</div>
					</div>

					<div class="w-full md:w-1/3 ">
            <div class="float-form">
              <h3 class="text-gray-700">Download today</h3>
              <BaseHubspot id="5e1bd485-7681-4c10-9ab9-e54d01c946d4" sfid="7011G000000UvDQQA0" />
            </div>
					</div>

				</div>
		</section>

		<GoCustomers />

  </Layout>
</template>

<script>

import GoCustomers from "~/components/GoCustomers.vue";
import Layout from '~/layouts/Landing.vue';

export default {
  metaInfo: {
    title: 'eBook: Replacing Netezza',
    meta: [
      {
        key: 'description',
        name: 'description',
        content: 'Download this eBook today to learn how Yellowbrick can help you achieve 100X performance, 10x scale, and save millions when replacing Netezza.'
      },
      {
        key: 'og:description',
        name: 'og:description',
        content: 'Download this eBook today to learn how Yellowbrick can help you achieve 100X performance, 10x scale, and save millions when replacing Netezza.'
      },
      {
        key: 'twitter:description',
        name: 'twitter:description',
        content: 'Download this eBook today to learn how Yellowbrick can help you achieve 100X performance, 10x scale, and save millions when replacing Netezza.'
      },
      {
        key: 'og:title',
        name: 'og:title',
        content: 'eBook: Replacing Netezza'
      },
      {
        key: 'twitter:title',
        name: 'twitter:title',
        content: 'eBook: Replacing Netezza'
      },
      {
        key: 'og:image',
        name: 'og:image',
        content: 'https://www.yellowbrick.com/uploads/ebook-netezza-thumb.jpg'
      },
      {
        key: 'twitter:image',
        name: 'twitter:image',
        content: 'https://www.yellowbrick.com/uploads/ebook-netezza-thumb.jpg'
      }
    ]
  },
  components: {
    GoCustomers,
    Layout
  }
};
</script>