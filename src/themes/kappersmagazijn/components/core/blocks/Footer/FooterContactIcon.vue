<template>
  <div>
    <h6><i :style="'background-image: url(' + icon + ')'" class="call-us" v-if="icon" />{{ title }}</h6>
    <a :href="url" class="outline-btn" v-if="type == 'email'">Stel hier je vraag</a>
    <div class="newsletter-input-container" v-if="type == 'newsletter'">
      <input type="text" name="newsletter" id="newsletter" placeholder="E-mailadres">
      <button type="submit">Aanmelden</button>
    </div>
    <a :href="url" :class="type" v-if="type !== 'email'"><span>{{ description }}</span></a> 
    <!-- @TODO There should be a better way to not show the above element if type is email. -->
  </div>
</template>

<style lang="scss" scoped>
@import "~theme/css/variables/colors";
@import "~theme/css/helpers/functions/color";

div {
  text-align: left;
}

h6 {
  i.call-us {
    display: inline-block;
    background-size: 20px 20px;
    height: 20px;
    width: 20px;
    background-repeat: no-repeat;
    margin-right: 20px;
  }

  color: #504538;
  line-height: 26px;
  margin-top: 0;
  margin-bottom: 1rem;
  font-weight: 500;
  font-size: 20px;
}

a {
  color: #504538;
  text-align: left;
}

.whatsapp {
  color: #BF512C;
  text-decoration: underline;
}

.newsletter-input-container {
  position: relative;

input {
    width: 100%;
    border: 1px solid #D9D9D9;
    border-radius: 6px;
    height: 53px;
    font-size: 16px;
    color: #7E7E7E;
    padding-left: 16px;
    padding-right: 145px;
  }

  button {
    position: absolute;
    right: 8px;
    height: 37px;
    top: 8px;
    background: color(secondary);
    border: none;
    border-radius: 6px;
    color: white;
    font-size: 16px;
    line-height: 26px;
    padding: 0 22px;
    transition: all .3s ease;

    &:hover {
      background: darken(color(secondary), 10%); // @TODO Don't know how to map the hover color
    }
  }
}
</style>

<script>
export default {
  props: [
    'title',
    'description',
    'url',
    'icon',
    'type'
  ]

}
</script>
