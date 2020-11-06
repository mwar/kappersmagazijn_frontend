<template>
  <div class="newsletter py25 px15 bg-cl-secondary" v-show="!isSubscribed">
    <form @submit.prevent="subscribe(onSuccesfulSubmission)" novalidate>
      <p class="h4">
        {{ $t('Sign up to our newsletter') }}
      </p>
      <base-input
        focus
        type="email"
        name="email"
        v-model="email"
        autocomplete="email"
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
      />
      <button-full
        class="mb35"
        type="submit"
        :disabled="this.$v.$invalid"
        @click.native="$v.email.$touch"
      >
        {{ $t('Subscribe') }}
      </button-full>
    </form>
  </div>
</template>

<script>
import SubscriptionStatus from '@vue-storefront/core/modules/newsletter/mixins/SubscriptionStatus'
import ButtonOutline from 'theme/components/theme/ButtonOutline'
import { mapState } from 'vuex'
import ButtonFull from 'theme/components/theme/ButtonFull.vue'
import BaseInput from 'theme/components/core/blocks/Form/BaseInput.vue'

const NewsletterPopup = () => import(/* webpackChunkName: "vsf-newsletter-modal" */ 'theme/components/core/NewsletterPopup.vue')

export default {
  name: 'Newsletter',
  mixins: [SubscriptionStatus],
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
      this.$bus.$emit('modal-show', 'modal-newsletter')
    }
  },
  components: {
    ButtonOutline,
    NewsletterPopup,
    ButtonFull,
    BaseInput
  }
}
</script>

<style scoped>
@media (min-width: 767px) and (max-width: 1200px) {
  .button-outline {
    min-width: 100%;
  }
}

@media (max-width: 767px) {
  .h3 {
    font-size: 18px;
    text-align: center;
  }

  .newsletter-button {
    padding-top: 25px;
    text-align: center;
  }
}
</style>
