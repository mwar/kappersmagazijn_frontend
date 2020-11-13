<template>
  <div class="relative base-input">
    <div class="relative input-control">
      <input
        class="
         py10 w-100 border-box brdr-none brdr-bottom-1
         brdr-cl-primary h4
       "
        :class="{pr30: type === 'password', empty: value === ''}"
        :type="type === 'password' ? passType : type"
        :name="name"
        :autocomplete="autocomplete"
        :value="value"
        :autofocus="autofocus"
        :ref="name"
        @input="$emit('input', $event.target.value)"
        @blur="$emit('blur')"
        @keyup.enter="$emit('keyup.enter', $event.target.value)"
        @keyup="$emit('keyup', $event)"
      >
      <label>{{ placeholder }}</label>
      <button-full :type="buttontype"
        class="no-outline button-full ripple weight-400 cl-white fs-medium ripple-dark"
        color="light" :link="link">{{ buttontext }}</button-full>
    </div>
    <ValidationMessages v-if="validations" :validations="validations" />
  </div>
</template>

<script>
import ValidationMessages from './ValidationMessages.vue'
import ButtonFull from '../../../theme/ButtonFull'

export default {
  name: 'BaseInputButton',
  components: {
    ButtonFull,
    ValidationMessages
  },
  data () {
    return {
      passType: 'password',
      iconActive: true,
      icon: 'visibility_off'
    }
  },
  props: {
    type: {
      type: String,
      required: true
    },
    value: {
      type: [String, Number],
      default: ''
    },
    name: {
      type: String,
      required: false,
      default: ''
    },
    placeholder: {
      type: String,
      required: false,
      default: ''
    },
    autocomplete: {
      type: String,
      required: false,
      default: ''
    },
    focus: {
      type: Boolean,
      required: false,
      default: false
    },
    autofocus: {
      type: Boolean,
      required: false,
      default: false
    },
    buttontext: {
      type: String,
      required: true,
      default: ''
    },
    buttontype: {
      type: String,
      required: false,
      default: 'button'
    },
    link: {
      type: String,
      default: null,
      required: false
    },
    validations: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    togglePassType () {
      if (this.passType === 'password') {
        this.passType = 'text'
        this.icon = 'visibility'
      } else {
        this.passType = 'password'
        this.icon = 'visibility_off'
      }
    },
    // setFocus sets focus on a field which has a value of 'ref' tag equal to fieldName
    setFocus (fieldName) {
      if (this.name === fieldName) {
        this.$refs[this.name].focus()
      }
    }
  },
  created () {
    if (this.type === 'password') {
      this.iconActive = true
    }
  },
  mounted () {
    if (this.focus) {
      this.$refs[this.name].focus()
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '~theme/css/variables/colors';
  @import '~theme/css/helpers/functions/color';
  $color-secondary: color(secondary);
  $color-secondary-hover: color(secondary, $colors-background);
  $color-tertiary: color(tertiary);
  $color-black: color(black);
  $color-puerto-rico: color(orange-brown);
  $color-hover: color(secondary, $colors-background);

  $dark-border: color(secondary);
  $white: color(white);
  $black: color(orange-brown);

  .base-input {
    min-height: 4.5rem;
  }

  .input-control {
    display: flex;
    flex-wrap: wrap;
    align-items: stretch;
    width: 100%;
    border: 1px solid $color-tertiary;
    border-radius: 6px;
    padding: 5px;
    height: 45px;

    .button-full {
      background-color: $color-secondary;
      display: flex;
      border-radius: 6px;
      font-weight: normal;
      font-size: 14px;
      padding: 0 10px;
      width: auto;
      height: 32px;
      &:hover {
        background-color: $color-hover;
      }
    }
  }

  input {
    flex: 1 1 auto;
    width: 1%;
    background: inherit;
    border: none;
    height: 35px;
    font-size: 14px ;

    &:hover,
    &:focus {
      outline: none;
      border: none;
    }

    &:disabled,
    &:disabled + label {
      opacity: 0.5;
      cursor: not-allowed;
      pointer-events: none;
    }
  }
  .button-full {
    display: flex;
    width: 20%;
    min-width: 10px;
  }
  label {
    color:#999;
    position:absolute;
    pointer-events:none;
    user-select: none;
    left: 10px;
    top: 12px;
    transition:0.2s ease all;
    -moz-transition:0.2s ease all;
    -webkit-transition:0.2s ease all;
  }
  input:focus ~ label, input:not(.empty) ~ label{
    top: -10px;
    font-size:14px;
    color:$color-puerto-rico;
    background-color: $white;
    margin-left: 2px;
    padding-left: 3px;
    padding-right: 3px;
  }

  .icon {
    right: 6px;
    top: 10px;
    &:hover,
    &:focus {
      color: $color-hover;
    }
  }
</style>
