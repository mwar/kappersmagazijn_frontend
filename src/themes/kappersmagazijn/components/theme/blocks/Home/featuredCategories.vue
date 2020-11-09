<template>
  <section class="featured-categories">
    <div class="container">
      <div class="row">
        <div class="col-xs-12">
          <h3>Bekijk alle kappersproducten per categorie</h3>
        </div>
      </div>

      <div class="row">
        <div class="col-xs-12 col-sm-6 col-md-3 col-lg-2">
          <div class="category-block">
            <div class="category-icon">
              <i class="chair-mirror"></i>
            </div>
            <div class="category-name">
              Kappersbenodigdheden
            </div>
          </div>
        </div>
        <div class="col-xs-12 col-sm-6 col-md-3 col-lg-2">
          <div class="category-block">
            <div class="category-icon">
              <i class="hairdyer-comb"></i>
            </div>
            <div class="category-name">
              Haarproducten
            </div>
          </div>
        </div>
        <div class="col-xs-12 col-sm-6 col-md-3 col-lg-2">
          <div class="category-block">
            <div class="category-icon">
              <i class="shaver"></i>
            </div>
            <div class="category-name">
              Scheren &amp; Messen
            </div>
          </div>
        </div>
        <div class="col-xs-12 col-sm-6 col-md-3 col-lg-2">
          <div class="category-block">
            <div class="category-icon">
              <i class="spray-bottle"></i>
            </div>
            <div class="category-name">
              Facilitair
            </div>
          </div>
        </div>
        <div class="col-xs-12 col-sm-6 col-md-3 col-lg-2">
          <div class="category-block">
            <div class="category-icon">
              <i class="spray-bottle-can"></i>
            </div>
            <div class="category-name">
              Geschenken
            </div>
          </div>
        </div>
        <div class="col-xs-12 col-sm-6 col-md-3 col-lg-2">
          <div class="category-block">
            <div class="category-icon">
              <i class="sale-tag"></i>
            </div>
            <div class="category-name">
              Aanbiedingen
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
export default {
  components: {},
  methods: {}
};
</script>
<style lang="scss" scoped>
section.featured-categories {
  padding: 64px 0;

  .category-block {
    background: #f8f8f8;
    border-radius: 6px;
    padding: 32px;
    color: #504538;
    font-size: 20px;
    line-height: 24px;

    &:hover {
      cursor: pointer;
      box-shadow: 0px 0px 10px #00000029;

      .category-icon > i {
        filter: invert(25%) sepia(7%) saturate(1463%) hue-rotate(352deg) brightness(99%) contrast(90%);
      }
    }

    .category-icon {
      height: 75px;
      margin-bottom: 18px;
      display: flex;
      justify-content: center;

      i {
        transition: all .3s ease;
        filter: invert(10%) sepia(0%) saturate(1826%) hue-rotate(235deg) brightness(116%) contrast(79%);
      }
    }

    .category-name {
      text-align: center;
    }
  }
}
</style>
