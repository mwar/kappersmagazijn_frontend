<template>
  <div class="newsletter" v-show="!isSubscribed">
    <form @submit.prevent="subscribe(onSuccesfulSubmission)" novalidate>
      <p><i class="email-us"></i> {{ $t('Sign up to our newsletter') }}</p>
      <base-input-button
        focus
        class="fs-big"
        type="email"
        name="email"
        v-model="email"
        autocomplete="email"
        :buttontext="$t('Subscribe')"
        :buttontype="subscribe(onSuccesfulSubmission)"
        :placeholder="$t('E-mail address *')"
        :validations="[
              {
                condition: $v.email.$error && !$v.email.required,
                text: $t('Field is required.')
              },
              {
                condition: !$v.email.email && $v.email.$error,
                text: $t('Please provide valid e-mail address.')
              }
            ]"
      >
      </base-input-button>
    </form>
  </div>
</template>

<script>
import SubscriptionStatus from '@vue-storefront/core/modules/newsletter/mixins/SubscriptionStatus'
import ButtonOutline from 'theme/components/theme/ButtonOutline'
import { mapState } from 'vuex'
import ButtonFull from 'theme/components/theme/ButtonFull.vue'
import BaseInput from 'theme/components/core/blocks/Form/BaseInput.vue'
import BaseInputButton from '../Form/BaseInputButton'
import i18n from '@vue-storefront/i18n'
import Subscribe from '@vue-storefront/core/modules/newsletter/mixins/Subscribe'

const NewsletterPopup = () => import(/* webpackChunkName: "vsf-newsletter-modal" */ 'theme/components/core/NewsletterPopup.vue')

export default {
  name: 'Newsletter',
  mixins: [SubscriptionStatus, Subscribe],
  data() {
    return {
      loadNewsletterPopup: false
    }
  },
  computed: {
    ...mapState({
      isOpen: state => state.ui.newsletterPopup
    })
  },
  methods: {
    showNewsletterPopup() {
      this.loadNewsletterPopup = true
    },
    onSuccesfulSubmission (isSubscribed) {
      if (isSubscribed) {
        this.$store.dispatch('notification/spawnNotification', {
          type: 'success',
          message: i18n.t('You have been successfully subscribed to our newsletter!'),
          action1: { label: i18n.t('OK') }
        })
      }
    }
  },
  components: {
    BaseInputButton,
    ButtonOutline,
    NewsletterPopup,
    ButtonFull,
    BaseInput
  }
}
</script>

<style lang="scss" scoped>
div {
  text-align: left;
  font-size: 14px;
}
p {
  i.email-us {
    display: inline-block;
    background-image: url(/assets/icons/sale-tag.svg);
    background-size: 20px 20px;
    height: 20px;
    width: 20px;
    background-repeat: no-repeat;
    margin-right: 20px;
  }

  margin: auto auto 25px;
  font-weight: normal;
  font-size: 20px;
}
</style>
