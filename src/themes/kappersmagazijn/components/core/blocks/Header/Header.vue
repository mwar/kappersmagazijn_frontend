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
          <div class="col-xs-11 col-md-6 col-lg-7">
            <div class="search-input">
              <input
                type="text"
                placeholder="waar ben je naar op zoek?"
                :aria-label="$t('Open search panel')"
                @focus="toggleSearchpanel"
                data-testid="openSearchPanel"
              />
            </div>
          </div>
          <div class="col-xs-6 col-md-4 col-lg-3">
            <ul class="header-menu">
              <li><commercial-icon /></li>
              <li><account-icon /></li>
              <li><wishlist-icon /></li>
              <li><microcart-icon /></li>
            </ul>
          </div>
        </div>
      </div>

      <div class="container">
        <div class="row">
          <div class="col-xs-12">
            <ul class="main-nav">
              <li class="has-children">
                <a href="#">Merk</a>
              </li>

              <li class="has-children">
                <a href="#">Haarproducten</a>
              </li>

              <li class="has-children">
                <a href="#">Kappersbenodigdheden</a>
              </li>

              <li class="has-children">
                <a href="#">Scheren &amp; Messen</a>
              </li>

              <li class="has-children">
                <a href="#">Facilitair</a>
              </li>

              <li class="has-children">
                <a href="#">Geschenken</a>
              </li>

              <li class="has-children">
                <a href="#">Interieur</a>
              </li>

              <li class="has-children highlight">
                <a href="#">Aanbiedingen</a>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <div class="usp-bar-container">
        <div class="container">
          <div class="row">
            <div class="col-xs-12">
              <ul class="usp-bar">
                <li>Vandaag besteld, morgen in huis</li>
                <li>30 dagen lang bedenktijd</li>
                <li>Klanten beoordelen ons met een 9,5!</li>
                <li>Punten sparen voor gratis producten</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </header>
    <!-- Header placeholder is for the distance behind the header -->
    <div class="header-placeholder" />
  </div>
</template>

<script>
import { mapState } from "vuex";
import CurrentPage from "theme/mixins/currentPage";
import AccountIcon from "theme/components/core/blocks/Header/AccountIcon";
import CompareIcon from "theme/components/core/blocks/Header/CompareIcon";
import HamburgerIcon from "theme/components/core/blocks/Header/HamburgerIcon";
import Logo from "theme/components/core/Logo";
import MicrocartIcon from "theme/components/core/blocks/Header/MicrocartIcon";
import CommercialIcon from "theme/components/core/blocks/Header/CommercialIcon";
import WishlistIcon from "theme/components/core/blocks/Header/WishlistIcon";

export default {
  name: "Header",
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
  data() {
    return {
      navVisible: true,
      isScrolling: false,
      scrollTop: 0,
      lastScrollTop: 0,
      navbarHeight: 54
    };
  },
  computed: {
    ...mapState({
      isOpenLogin: state => state.ui.signUp,
      currentUser: state => state.user.current
    }),
    isThankYouPage() {
      return this.$store.state.checkout.isThankYouPage
        ? this.$store.state.checkout.isThankYouPage
        : false;
    }
  },
  beforeMount() {
    window.addEventListener(
      "scroll",
      () => {
        this.isScrolling = true;
      },
      { passive: true }
    );

    setInterval(() => {
      if (this.isScrolling) {
        this.hasScrolled();
        this.isScrolling = false;
      }
    }, 250);
  },
  methods: {
    gotoAccount() {
      this.$bus.$emit("modal-toggle", "modal-signup");
    },
    hasScrolled() {
      this.scrollTop = window.scrollY;
      if (
        this.scrollTop > this.lastScrollTop &&
        this.scrollTop > this.navbarHeight
      ) {
        this.navVisible = false;
      } else {
        this.navVisible = true;
      }
      this.lastScrollTop = this.scrollTop;
    },
    toggleSearchpanel() {
      this.$store.commit("ui/setSearchpanel", true);
    }
  }
};
</script>

<style lang="scss" scoped>
@import "~theme/css/variables/colors";
@import "~theme/css/helpers/functions/color";
$color-primary: color(primary, $colors-theme);

header {
  height: 199px;
  top: -85px;
  z-index: 3;
  border-top: 2px solid $color-primary;
  border-bottom: 1px solid #E5E3E1;
  transition: top 0.2s ease-in-out;
  &.is-visible {
    top: 0;
  }

  .search-input {
    position: relative;

    &::after {
      content: "";
      position: absolute;
      background-image: url("/assets/icons/search-regular.svg");
      background-size: 24px;
      height: 24px;
      width: 24px;
      right: 20px;
      top: calc(50% - 12px);
    }

    input {
      display: block;
      width: 100%;
      height: 42px;
      border: 1px solid #bbccdd;
      border-radius: 6px;
      padding: 0 20px;
      font-size: 1rem;
      line-height: 19px;
      font-family: "Cabin", sans-serif;

      &::placeholder {
        /* Chrome, Firefox, Opera, Safari 10.1+ */
        color: #bbccdd;
        opacity: 1; /* Firefox */
      }

      &:-ms-input-placeholder {
        /* Internet Explorer 10-11 */
        color: #bbccdd;
      }

      &::-ms-input-placeholder {
        /* Microsoft Edge */
        color: #bbccdd;
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

  ul.main-nav {
    padding: 0;
    list-style: none;
    margin-bottom: 0 0 20px 0;

    li {
      display: inline-block;
      position: relative;
      margin-right: 20px;
      text-transform: lowercase;

      &:hover {
        &.has-children {
          &::after {
            transform: rotate(180deg);
          }
        }
      }

      // If menu item has children
      &.has-children {
        padding-right: 26px;

        &::after {
          content: "";
          position: absolute;
          background-image: url("/assets/icons/chevron-down-light.svg");
          background-size: 16px 8px;
          height: 8px;
          width: 16px;
          right: 0;
          top: calc(50% - 4px);
          transition: transform .3s ease;
          cursor: pointer;
          filter: invert(24%) sepia(33%) saturate(318%) hue-rotate(352deg) brightness(98%) contrast(90%);
        }
      }

      &.highlight {

        &.has-children {
          &::after {
            filter: invert(35%) sepia(18%) saturate(3934%) hue-rotate(342deg) brightness(99%) contrast(85%);
          }
        }

        a {
          color: #BF512C;
          transition: color .3s ease;

          &:hover {
            color: lighten(#BF512C, 10%);
          }
        }
      }

      a {
        color: #504538;
        font-size: 20px;
        line-height: 24px;
        transition: color .3s ease;

        &:hover {
          color: lighten(#504538, 10%);
        }
      }
    }
  }

.usp-bar-container {
  border-top: 1px solid #E5E3E1;
  border-bottom: 1px solid #E5E3E1;

  ul.usp-bar {
    display: flex;
    justify-content: space-between;
    margin: 0;
    padding: 0;
    padding: 13px 0;
    list-style: none;
    background: white;

      li {
        color: #333333;
        font-size: 14px;
        line-height: 18px;
        padding-left: 32px;
        position: relative;

        &::before {
            content: "";
            position: absolute;
            background-image: url("/assets/icons/check-circle-solid.svg");
            filter: invert(22%) sepia(11%) saturate(1146%) hue-rotate(352deg) brightness(99%) contrast(81%);
            background-size: 20px;
            height: 20px;
            width: 20px;
            left: 0;
            top: calc(50% - 10px);
        }
      }
  }
}

}

.header-placeholder {
  height: 199px;
}
</style>
