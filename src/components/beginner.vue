<template>
<body>
  <section class="product">
    <article class="product-img">
      <img v-bind:src="image" alt />
    </article>

    <!-- description of the products  -->
    <article class="product-info">
      <h1>{{title}}</h1>

      <p v-if="inStock > 10">In Stock</p>
      <p v-else-if="inStock < 10 && inStock >0">Almost out of stock</p>
      <p v-else :class="{outOfStock:!inStock}">Out of Stock</p>
      <p>Shipping {{shipping}}</p>
      <productDetail @review-submitted="addReview" />

      <!-- <p v-show="inStock">It will be soon in stock</p> -->
      <!-- details of the products -->
      <article class="details">
        <ul>
          <li v-for="detail in details" :key="detail.index">{{ detail.type }}</li>
        </ul>
      </article>

      <!-- color-box of the products -->
      <article
        v-for="(variant, index) in variants"
        :key="variant.variantId"
        class="color-box"
        :style="{backgroundColor:variant.variantColor}"
        @mouseover="uppDateProduct(index)"
      >
        {{variant.variantColor}}
        <!-- cart  -->
      </article>

      <!-- button to add or sub the product from the cart -->
      <article class="button">
        <button v-on:click="addToCart" :disabled="!inStock" :class="{disabledButton:!inStock}">Add</button>
        <button v-on:click="removeItem" :disabled="!inStock" :class="{disabledButton:!inStock}">Less</button>
      </article>
    </article>
    <productReview @review-submitted="addReview" />
  </section>
  <section>
   
  
    <h2>Reviews</h2>
    <p v-if="!reviews.length">No reviews yet</p>
    <ul>
      <li v-for="(review, index)  in reviews" :key="index">
        <p>Name {{review.name}}</p>
        <p>Rating {{review.rating}}</p>
        <p>{{review.review}}</p>
      </li>
    </ul>
  </section>
</body>
</template>

<script>
import productDetail from "./details.vue";
import productReview from "./productReview.vue";
export default {
  name: "product",
  components: {
    productDetail,
    productReview,
  },
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      brand: "Karmacare",
      product: "Socks",
      description: "Socks for socker player",
      selectedVariant: 0,
      onSale: true,
      // invetory: 10,
      website: "www.karmacareshop.com",
      details: [
        { type: "cotton", index: 1 },
        { type: "plyester", index: 2 },
        { type: "Gender-natural", index: 3 },
      ],
      variants: [
        {
          variantId: 2234,
          variantColor: "green",
          variantImg:
            "https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg",
          variantQuantity: 15,
        },
        {
          variantId: 2235,
          variantColor: "blue",
          variantImg:
            "https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg",
          variantQuantity: 5,
        },
      ],
      reviews: [],
    };
  },
  methods: {
    checkStock() {
      if (this.invetory === 0) {
        this.inStock === true;
        console.log(this.invetory);
      } else {
        this.inStock === false;
      }
    },
    addToCart() {
      this.$emit("add-to-cart", this.variants[this.selectedVariant].variantId);
    },
    removeItem() {
      this.$emit(
        "remove-from-cart",
        this.variants[this.selectedVariant].variantId
      );
    },
    uppDateProduct(index) {
      this.selectedVariant = index;
      console.log(index);
    },
    addReview(productReview) {
      this.reviews.push(productReview);
    },
  },
  computed: {
    title() {
      return this.brand + " " + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImg;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity;
    },
    sale() {
      if (this.onSale) {
        return this.brand + " " + this.product + "are on sale";
      }
      return this.brand + " " + this.product + " are not on sale";
    },
    shipping() {
      if (this.premium) {
        return "free";
      }
      return 2.99 + "€";
    },
  },
};
</script>


<style  lang="scss">
body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
  .nav-bar {
    background: linear-gradient(-90deg, #84cf6a, #16c0b0);
    height: 60px;
    margin-bottom: 15px;
  }
  .product {
    display: flex;
    img {
      border: 1px solid #d8d8d8;
      width: 70%;
      margin: 40px;
      box-shadow: 0px 0.5px 1px #d8d8d8;
    }

    .product-img {
      flex-basis: 700px;
      a {
        text-decoration: none;
        color: #eee;
      }
    }

    .product-info {
      margin-top: 10px;
      flex-basis: 500px;
      .outOfStock {
        text-decoration: line-through;
      }
    }
    .color-box {
      width: 40px;
      height: 40px;
      margin-bottom: 5px;
    }

    button {
      margin-top: 30px;
      border: none;
      background-color: #1e95ea;
      color: white;
      height: 40px;
      width: 100px;
      font-size: 14px;
    }

    .disabledButton {
      background-color: #d8d8d8;
    }

    input {
      width: 100%;
      height: 25px;
      margin-bottom: 20px;
    }

    textarea {
      width: 100%;
      height: 60px;
    }
  }
}
</style>
