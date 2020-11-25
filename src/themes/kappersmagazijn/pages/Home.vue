<template>
  <div id="home">
    <featuredCategories />
    <featuredProducts />

    <section class="content-section">
      <div class="container">
        <div class="row">
            <div class="col-xs-12 col-md-offset-2 col-md-4">
            <div class="image-container pr20">
                    <img
                    src="https://picsum.photos/1200/900"
                    alt="Productnaam"
                    class="product-image">
            </div>
          </div>
          <div class="col-xs-12 col-md-4">
            <h3>De beste kappersproducten voor de laagste prijs</h3>

            <p>Door ons uitgebreide scala aan exclusieve merken met internationale bekendheid, heeft Kappersmagazijn zich ontwikkeld tot een ware trendsetter.</p>

            <p>Daarnaast onderscheidt Kappersmagazijn zich door kwaliteit, service en snelle levering. Hierdoor zijn wij al jaren een betrouwbare groothandel in kappersproducten met een zeer divers klantenbestand. Van de grote kapsalons, voor wie wij leverancier zijn van kappersstoelen tot gel, maar daarnaast ook de particulier die maandelijks zijn shampoos bij ons besteld.</p>

            <p>Kappersmagazijn wil namelijk iedereen het voordeel gunnen van haar topmerken en producten, zonder hierop een doelgroep uit te sluiten zoals de meeste groothandels. Immers als u tevreden bent, zijn wij dat ook.</p>

            <p>Mocht u ondanks de zorgvuldige samenstelling van deze webshop, toch nog vragen hebben over Kappersmagazijn of één van onze producten, neem dan gerust contact met ons op.</p>
          </div>
        </div>
      </div>
    </section>

    <section class="image-hero" style="background-image: url('https://picsum.photos/1200/900');">
      <h3>Voor al uw kappersproducten en benodigdheden</h3>
    </section>

    <!-- <section class="new-collection container px15">
      <div>
        <header class="col-md-12">
          <h2 class="align-center cl-accent">
            {{ $t('Everything new') }}
          </h2>
        </header>
      </div>

      <div class="row center-xs">
        <lazy-hydrate :trigger-hydration="!loading" v-if="isLazyHydrateEnabled">
          <product-listing columns="4" :products="getEverythingNewCollection" />
        </lazy-hydrate>
        <product-listing v-else columns="4" :products="getEverythingNewCollection" />
      </div>
    </section>

    <section v-if="isOnline" class="container pb60 px15">
      <div class="row center-xs">
        <header class="col-md-12" :class="{ pt40: getEverythingNewCollection && getEverythingNewCollection.length }">
          <h2 class="align-center cl-accent">
            {{ $t('Get inspired') }}
          </h2>
        </header>
      </div>
      <tile-links />
    </section>
    <Onboard /> -->
  </div>
</template>

<script>
// query constructor
import { isServer, onlineHelper } from '@vue-storefront/core/helpers'
import LazyHydrate from 'vue-lazy-hydration'

// Theme core components
import ProductListing from 'theme/components/core/ProductListing'
import HeadImage from 'theme/components/core/blocks/MainSlider/HeadImage'
// Theme local components
import Onboard from 'theme/components/theme/blocks/Home/Onboard'
import PromotedOffers from 'theme/components/theme/blocks/PromotedOffers/PromotedOffers'
import TileLinks from 'theme/components/theme/blocks/TileLinks/TileLinks'
import { Logger } from '@vue-storefront/core/lib/logger'
import { mapGetters } from 'vuex'
import config from 'config'
import { registerModule } from '@vue-storefront/core/lib/modules'
import { RecentlyViewedModule } from '@vue-storefront/core/modules/recently-viewed'
import featuredCategories from 'theme/components/theme/blocks/Home/featuredCategories'
import featuredProducts from 'theme/components/theme/blocks/Home/featuredProducts'

export default {
  data () {
    return {
      loading: true
    }
  },
  components: {
    Onboard,
    ProductListing,
    featuredCategories,
    featuredProducts,
    TileLinks,
    LazyHydrate
  },
  computed: {
    ...mapGetters('user', ['isLoggedIn']),
    ...mapGetters('homepage', ['getEverythingNewCollection']),
    categories () {
      return this.getCategories
    },
    isOnline () {
      return onlineHelper.isOnline
    },
    isLazyHydrateEnabled () {
      return config.ssr.lazyHydrateFor.some(
        field => ['homepage', 'homepage.new_collection'].includes(field)
      )
    }
  },
  beforeCreate () {
    registerModule(RecentlyViewedModule)
  },
  async beforeMount () {
    if (this.$store.state.__DEMO_MODE__) {
      const onboardingClaim = await this.$store.dispatch('claims/check', { claimCode: 'onboardingAccepted' })
      if (!onboardingClaim) { // show onboarding info
        this.$bus.$emit('modal-toggle', 'modal-onboard')
        this.$store.dispatch('claims/set', { claimCode: 'onboardingAccepted', value: true })
      }
    }
  },
  mounted () {
    if (!this.isLoggedIn && localStorage.getItem('redirect')) this.$bus.$emit('modal-show', 'modal-signup')
  },
  watch: {
    isLoggedIn () {
      const redirectObj = localStorage.getItem('redirect')
      if (redirectObj) this.$router.push(redirectObj)
      localStorage.removeItem('redirect')
    }
  },
  async asyncData ({ store, route, context }) { // this is for SSR purposes to prefetch data
    if (context) context.output.cacheTags.add(`home`)
    Logger.info('Calling asyncData in Home Page (core)')()

    await Promise.all([
      store.dispatch('homepage/fetchNewCollection'),
      store.dispatch('promoted/updateHeadImage'),
      store.dispatch('promoted/updatePromotedOffers')
    ])
  },
  beforeRouteEnter (to, from, next) {
    if (!isServer && !from.name) { // Loading products to cache on SSR render
      next(vm =>
        vm.$store.dispatch('homepage/fetchNewCollection').then(res => {
          vm.loading = false
        })
      )
    } else {
      next()
    }
  },
  metaInfo () {
    return {
      title: this.$route.meta.title || this.$i18n.t('Home Page'),
      meta: this.$route.meta.description ? [{ vmid: 'description', name: 'description', content: this.$route.meta.description }] : []
    }
  }
}
</script>

<style lang="scss" scoped>
  .new-collection {
    @media (max-width: 767px) {
      padding-top: 0;
    }
  }

  section.content-section {
    padding: 64px 0;

    h3 {
      font-weight: bold;
    }

    .image-container {
      height: 100%;

      img {
        width: 100%;
        height: 100%;
        object-fit: cover;
        border-radius: 6px;
      }
    }
  }

  section.image-hero {
    height: 50vh;
    background-size: cover;
    background-position: center;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;

    &::after {
      content: '';
      position: absolute;
      top: 0;
      width: 100%;
      height: 100%;
      backdrop-filter: blur(1px);
    }

    h3 {
      color: #FFFFFF;
      text-shadow: 0px 8px 15px #00000029;
      display: flex;
      flex-direction: row;
      width: 90%;
      font-size: 38px;
      line-height: 50px;
      z-index: 1;

      &::before, &::after {
        content: "";
        flex: 1 1;
        border-bottom: 2px solid #fff;
        margin: auto;
      }

      &::before {
        margin-right: 3rem;
      }

      &::after {
        margin-left: 3rem;
      }
    }
  }
</style>
