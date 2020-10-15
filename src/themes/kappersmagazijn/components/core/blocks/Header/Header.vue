<template>
  <div class="header">
    <header
      class="fixed w-100 brdr-bottom-1 bg-cl-primary brdr-cl-secondary"
      :class="{ 'is-visible': navVisible }"
    >
      <div class="container">
        <div class="row pt16 pb16">
          <div class="col-xs-6 col-md-2">
            <div>
              <logo width="auto" height="59px" />
            </div>
          </div>
          <div class="col-xs-12 col-md-6">
            <div class="search-input">
              <input type="text" placeholder="waar ber ben je naar op zoek?" />
            </div>
          </div>
          <div class="col-xs-6 col-md-4">
            <search-icon class="p15 icon hidden-xs pointer" />
            <wishlist-icon class="p15 icon hidden-xs pointer" />
            <compare-icon class="p15 icon hidden-xs pointer" />
            <microcart-icon class="p15 icon pointer" />
            <account-icon class="p15 icon hidden-xs pointer" />
          </div>
        </div>
      </div>
    </header>
    <div class="header-placeholder" />
  </div>
</template>

<script>
import { mapState } from 'vuex'
import CurrentPage from 'theme/mixins/currentPage'
import AccountIcon from 'theme/components/core/blocks/Header/AccountIcon'
import CompareIcon from 'theme/components/core/blocks/Header/CompareIcon'
import HamburgerIcon from 'theme/components/core/blocks/Header/HamburgerIcon'
import Logo from 'theme/components/core/Logo'
import MicrocartIcon from 'theme/components/core/blocks/Header/MicrocartIcon'
import SearchIcon from 'theme/components/core/blocks/Header/SearchIcon'
import WishlistIcon from 'theme/components/core/blocks/Header/WishlistIcon'

export default {
  name: 'Header',
  components: {
    AccountIcon,
    CompareIcon,
    HamburgerIcon,
    Logo,
    MicrocartIcon,
    SearchIcon,
    WishlistIcon
  },
  mixins: [CurrentPage],
  data () {
    return {
      navVisible: true,
      isScrolling: false,
      scrollTop: 0,
      lastScrollTop: 0,
      navbarHeight: 54
    }
  },
  computed: {
    ...mapState({
      isOpenLogin: state => state.ui.signUp,
      currentUser: state => state.user.current
    }),
    isThankYouPage () {
      return this.$store.state.checkout.isThankYouPage
        ? this.$store.state.checkout.isThankYouPage
        : false
    }
  },
  beforeMount () {
    window.addEventListener(
      'scroll',
      () => {
        this.isScrolling = true
      },
      { passive: true }
    )

    setInterval(() => {
      if (this.isScrolling) {
        this.hasScrolled()
        this.isScrolling = false
      }
    }, 250)
  },
  methods: {
    gotoAccount () {
      this.$bus.$emit('modal-toggle', 'modal-signup')
    },
    hasScrolled () {
      this.scrollTop = window.scrollY
      if (
        this.scrollTop > this.lastScrollTop &&
        this.scrollTop > this.navbarHeight
      ) {
        this.navVisible = false
      } else {
        this.navVisible = true
      }
      this.lastScrollTop = this.scrollTop
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~theme/css/variables/colors';
@import '~theme/css/helpers/functions/color';
$color-primary: color(primary, $colors-theme);

header {
  height: 130px;
  top: -55px;
  z-index: 3;
  border-top: 2px solid $color-primary;
  transition: top 0.2s ease-in-out;
  &.is-visible {
    top: 0;
  }

  .search-input {
    input {
      display: block;
      width: 100%;
      height: 42px;
      border: 1px solid #BBCCDD;
      border-radius: 6px;
      padding: 13px 20px;
    }
  }
}
</style>
