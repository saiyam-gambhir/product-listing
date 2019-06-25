<template>
  <section class="products-listing-section">
    <div v-for="product in products" :key="product.id" class="product">
      <div class="product-inner" v-if="!processing">
        <span class="product-tag" v-if="product.on_sale == 'true'">
          {{ salePercentage(product.sale_price, product.price) }}% off
        </span>
        <a :href="product.url">
          <figure class="product-figure">
            <img :src="product.ssProductData[0].biggerImageUrl" alt="">
          </figure>
        </a>
        <h2 class="h2 product-name">
          {{ product.name }}
        </h2>
        <div class="product-price-section">
          <h3 class="product-sale-price" v-if="product.sale_price > 0">From ${{ product.sale_price }}</h3>
          <h3 class="product-price" :class="{ original: product.sale_price > 0 }">${{ product.price }}</h3>
        </div>
        <p class="product-options">{{ product.ssProductData.length }} options available</p>
        <ul class="product-swatches">
          <li v-for="item in product.sortedSSProductData" :key="item.id" :title="item.swatch_colour">
            <img :src="item.swatch" alt="">
          </li>
        </ul>
      </div>
      <div v-else class="loading-product">
        <div class="figure"></div>
        <div class="name"></div>
        <div class="price"></div>
        <div class="options"></div>
      </div>
    </div>
  </section>
</template>

<script>
  export default {
    props: {
      products: Array,
      processing: Boolean
    },

    methods: {
      salePercentage (sale_price, price) {
        return Math.floor(100 - (sale_price*100/price))
      }
    }
  }
</script>

<style scoped>
  .products-listing-section {
    display: flex;
    flex-wrap: wrap;
    margin: 0 auto;
    width: 1200px;
  }

  .product {
    flex-basis: calc(25% - 30px);
    flex-grow: 1;
    margin: 22px 15px;
    position: relative;
  }

  .full-width {
    width: 100%;
  }

  .product-figure,
  .loading-product .figure {
    background: #f8f8f9;
    height: 200px;
    margin: 0;
    width: 100%;
    text-align: center;
  }

  .loading-product .name,
  .loading-product .price,
  .loading-product .options {
    background: #f8f8f9;
    height: 10px;
    margin-top: 10px;
    width: 75%;
  }

  .loading-product .price {
    width: 65%;
  }

  .loading-product .options {
    width: 55%;
  }

  .product-name {
    font-size: 15px;
    font-weight: 400;
    margin: 0;
    padding: 10px 0 7px 0;
  }

  .product-tag {
    background: #e04747;
    color: #fff;
    position: absolute;
    right: 0;
    top: 0;
    font-size: 12px;
    font-weight: 700;
    padding: 5px 10px;
  }

  .product-price-section {
    display: flex;
  }

  .product-sale-price,
  .product-price {
    color: #e04747;
    font-size: 15px;
    font-weight: 700;
    margin: 0;
  }

  .product-price {
    color: #2b2b2b;
  }

  .product-price.original {
    color: #bbbbbb;
    margin-left: 7px;
    text-decoration: line-through;
  }

  .product-options {
    color: #c7c7c7;
    font-size: 12px;
  }

  .product-swatches {
    margin: 20px -3px;
    padding: 0;
    display: flex;
    flex-wrap: wrap;
  }

  .product-swatches li {
    list-style: none;
    cursor: pointer;
    margin: 3px;
  }

  .product-swatches img {
    border-radius: 50%;
    width: 24px;
    height: 24px;
  }
</style>
