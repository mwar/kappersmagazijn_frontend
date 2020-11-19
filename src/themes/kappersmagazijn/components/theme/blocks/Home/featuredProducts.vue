<template>
  <section class="featured-products">
    <div class="container">
      <div class="row">
        <div class="col-xs-12">
          <h3>Uitgelichte producten</h3>
        </div>
      </div>

      <div class="row">
        <div class="col-xs-12 col-sm-6 col-md-3 col-lg-2">
          <div class="product-block">
            <button id="favorite" class="favorites-btn"><i class="favorites"></i></button>
            <a href="#" class="stretched-link">
              <div class="product-image-container">
                <img
                  src="https://picsum.photos/1200/1200"
                  alt="Productnaam"
                  class="product-image"
                >
              </div>
            </a>
            <div class="product-labels">
              <ul class="labels">
                <li class="discount">-25%</li>
                <li class="sustainable">Duurzaam</li>
              </ul>
            </div>
            <div class="product-details">
              <h4>Productnaam</h4>
              <div class="product-price">
                <span class="old-price">79.95</span>
                <span class="price">79.95</span>
              </div>
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
section.featured-products {
  padding: 64px 0;
  background: #745e431a;

  .product-block {
    background: white;
    border-radius: 6px;
    position: relative;

    .favorites-btn {
      background: none;
      border: none;
      position: absolute;
      z-index: 1;
      top: 15px;
      right: 15px;
      transition: all .5s ease;

      &:hover {
        i {
          filter: invert(33%) sepia(51%) saturate(1974%) hue-rotate(336deg) brightness(103%) contrast(88%);
        }
      }

      i {
        filter: invert(99%) sepia(0%) saturate(1414%) hue-rotate(227deg) brightness(80%) contrast(90%);
      }
    }

    .product-image-container {
      height: 250px;

      img.product-image {
        width: 100%;
        height: 100%;
        object-fit: cover;
        border-top-left-radius: 6px;
        border-top-right-radius: 6px;
      }
    }

    .product-labels {
      ul.labels {
        padding: 0;
        list-style: none;
        margin: 13px 0;

        li {
          display: inline-block;
          font-size: 16px;
          line-height: 19px;
          padding: 5px 10px;

          &.discount {
            color: white;
            background: #bf512c;
          }

          &.sustainable {
            color: #118844;
            background: #f3f9f6;
          }
        }
      }
    }

    .product-details {
      padding: 0 10px 10px 10px;

      h4 {
        font-size: 16px;
        line-height: 18px;
      }

      .product-price {
        span {
          &.price {
            font-size: 16px;
            line-height: 19px;
            color: #bf512c;
          }

          &.old-price {
            color: #556677;
            font-size: 14px;
            line-height: 18px;
            text-decoration:line-through;
          }

          &:not(:last-child) {
            margin-right: 6px;
          }
        }
      }
    }
  }
}

.stretched-link {
  &::after {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 1;
    pointer-events: auto;
    content: "";
    background-color: rgba(0, 0, 0, 0);
  }
}
</style>
