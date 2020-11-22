<template>
  <div class="footer-block">
    <h5 :class="{ active: isActive }" @click="isActive = !isActive">
      {{ title }}
    </h5>
    <!-- BEGIN CMS BLOK -->
    <div :class="{ active: isActive}" class="link-list">
      <slot>
        List
      </slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FooterLinks',
  props: {
    title: {
      type: String,
      required: true
    }
  },
  data: function () {
    return {
      isActive: false
    };
  },
  methods: {}
}
</script>

<style lang="scss" scoped>
@import '~theme/css/variables/colors';
@import '~theme/css/helpers/functions/color';

$color-white: color(white-smoke);
h5 {
  width: 100%;
  height: 20px; /* TODO Klopt dit wel */
  padding: 0;
  margin: 0;
}

ul {
  margin: 0;
  padding: 0;
  list-style: none;

  li {
    text-align: left;
  }
}

@media screen and (max-width: 768px) {
  .footer-block {
    width: 100%;
    padding: 2px 0;
    margin-bottom: 10px;
  }
  h5 {
    display: inline-block;
    padding: 5px 0;
    width: 100%;
    font-weight: normal;
    font-size: medium;

    &::after {
      content: "";
      position: absolute;
      background-image: url("/assets/icons/chevron-down-light.svg");
      background-size: 16px 8px;
      margin-top: 5px;
      height: 8px;
      width: 16px;
      right: 60px;
      transition: transform .3s ease;
      cursor: pointer;
      filter: invert(24%) sepia(33%) saturate(318%) hue-rotate(352deg) brightness(98%) contrast(90%);
    }

    &.active {
      &::after {
        transform: rotate(180deg);
      }
    }
  }
  div.link-list {
    display: none;

    &.active {
      display: inherit;
    }

    li {
      a {
        color: $color-white;
      }

      padding: 2px 10px;
    }
  }
}

</style>
