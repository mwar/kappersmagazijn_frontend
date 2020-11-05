<template>
  <div class="header">
    <header
      class="fixed w-100 brdr-bottom-1 bg-cl-primary brdr-cl-secondary"
      :class="{ 'is-visible': navVisible }"
    >
      <div class="container">
        <div class="row pt16 pb16 middle-xs">
          <div class="col-xs-6 col-md-2">
            <div>
              <logo width="auto" height="59px" />
            </div>
          </div>
          <div class="col-xs-12 col-md-6">
            <div class="search-input">
              <input type="text" placeholder="waar ben je naar op zoek?" :aria-label="$t('Open search panel')" @focus="toggleSearchpanel" data-testid="openSearchPanel">
            </div>
          </div>
          <div class="col-xs-6 col-md-4">
            <ul class="header-menu">
              <li><commercial-icon /></li>
              <li><account-icon /></li>
              <li><wishlist-icon /></li>
              <li><microcart-icon /></li>
            </ul>
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
import CommercialIcon from 'theme/components/core/blocks/Header/CommercialIcon'
import WishlistIcon from 'theme/components/core/blocks/Header/WishlistIcon'

export default {
  name: 'Header',
  components: {
    AccountIcon,
    CompareIcon,
    // HamburgerIcon,
    Logo,
    MicrocartIcon,
    CommercialIcon,
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
    },
    toggleSearchpanel () {
      this.$store.commit('ui/setSearchpanel', true)
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
    position: relative;

    &::after {
      content: '';
      position: absolute;
      background-image: url('/assets/icons/search-regular.svg');
      background-size: 24px;
      height: 24px;
      width: 24px;
      right: 20px;
      top: calc(50% - 12px);
    }

    input {
      display: block;
      width: 100%;
      height: 40px;
      border: 1px solid #BBCCDD;
      border-radius: 6px;
      padding: 0 20px;
      font-size: 1rem;
      line-height: 19px;
      font-family: 'Cabin', sans-serif;

      &::placeholder { /* Chrome, Firefox, Opera, Safari 10.1+ */
        color: #BBCCDD;
        opacity: 1; /* Firefox */
      }

      &:-ms-input-placeholder { /* Internet Explorer 10-11 */
        color: #BBCCDD;
      }

      &::-ms-input-placeholder { /* Microsoft Edge */
        color: #BBCCDD;
      }
    }
  }

  ul.header-menu {
    margin: 0;
    padding: 0;
    list-style: none;
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    margin-left: 2rem;

    li {
      display: inline-block;
    }
  }
}

.header-placeholder {
  height: 130px;
}
</style>
