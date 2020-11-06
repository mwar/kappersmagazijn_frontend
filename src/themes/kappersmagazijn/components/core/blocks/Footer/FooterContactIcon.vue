<template>
  <div>
    <h6><i :style="'background-image: url(' + icon + ')'" class="call-us"/>{{ title }}</h6>
    <a :href="url"><span>{{ description }}</span></a>
  </div>
</template>

<style lang="scss" scoped>
div {
  text-align: left;
}

h6 {
  i.call-us {
    display: inline-block;
    //background-image: url(/assets/icons/search-regular.svg);
    background-size: 20px 20px;
    height: 20px;
    width: 20px;
    background-repeat: no-repeat;
    //margin: 0 auto 5px auto;
    margin-right: 20px;
  }

  line-height: 15px;
  margin: auto auto 15px;
  font-weight: normal;
  font-size: large;
}

a {
  color: #504538;
  text-align: left;
}
</style>

<script>
export default {
  props: [
    'title',
    'description',
    'url',
    'icon'
  ]

}
</script>
