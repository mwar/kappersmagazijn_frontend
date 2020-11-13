<template>
  <div class="footer-call-us">
    <p><i class="email-us"></i>{{ $t('Call us')}}</p>
    <a href="tel:+31503642377">050 364 23 77</a>
  </div>
</template>

<style lang="scss" scoped>
@import "~theme/css/variables/colors";
@import "~theme/css/helpers/functions/color";
$color-primary: color(orange-brown, $colors);
$color-secondary: color(white, $colors);

div {
  text-align: left;
}

p {
  i.email-us {
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
  color: #504538;
  text-align: left;
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
