<template>
  <div class="align-left footer-message-us">
    <p><i class="whatsapp"></i>{{ $t('WhatsApp us')}}</p>
    <a  class="underline" href="tel:+3150364237">{{ $t('Click here to send us an message')}}</a>
  </div>
</template>

<style lang="scss" scoped>
@import "~theme/css/variables/colors";
@import "~theme/css/helpers/functions/color";
$color-primary: color(orange-brown, $colors);

p {
  i.whatsapp {
    display: inline-block;
    background-image: url(/assets/icons/sale-tag.svg);
    background-size: 20px 20px;
    height: 20px;
    width: 20px;
    background-repeat: no-repeat;
    //margin: 0 auto 5px auto;
    margin-right: 20px;
  }

  margin: auto auto 25px;
  font-weight: normal;
  font-size: 20px;
}

a {
  color: $color-primary;
  text-align: left;

  &.underline:after {
    background-color: $color-primary;
  }
}
</style>

<script>
import ButtonOutline from '../../../theme/ButtonOutline'
import { localizedRoute } from '@vue-storefront/core/lib/multistore'
export default {
  components: { ButtonOutline },
  props: [
    'title',
    'description',
    'url',
    'icon'
  ]

}
</script>
