<template>
  <div class="product">
    <div class="product-image">
      <img :src="image" :alt="altText"/>
    </div>

    <div class="product-info">
      <h1>{{ title }}</h1>
			<p>{{ description }}</p>
      <p v-if="inStock" >In stock</p>
      <p v-else :class="{ outOfStock: !inStock }">Out of Stock</p>
      <p>Shipping: {{ shipping }}</p>
			<p>User is premium: {{ premium }}</p>
			<p>{{ sale }}</p>
			<a :href="link">Перейди по ссылке для деньги бесплатно!</a>
      <ul>
        <li v-for="detail in details" :key="detail">{{ detail }}</li>
      </ul>
			<ul>
        <li v-for="size in sizes" :key="size">{{ size }}</li>
      </ul>
			<span v-if="onSale">Скидка!!!!</span>
      <div
        class="color-box"
        v-for="(variant, index) in variants"
        :key="variant.variantId"
        :style="{ backgroundColor: variant.variantColor }"
        @mouseover="updateProduct(index)"
      ></div>

      <button
        v-on:click="addToCart"
        :disabled="!inStock"
        :class="{ disabledButton: !inStock }"
      >
        Add to cart
      </button>
			<button
				@click="MinCart"
				class="delete"
			>
			Delete to Cart
			</button>

      <div class="cart">
        <p>Cart({{ cart }})</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  el: '#app',
  data() {
		return {
    product: 'Socks',
    brand: 'Vue Mastery',
    selectedVariant: 0,
		altText: 'The socks',
		shipping: 'Free',
		onSale: true,
		link: 'https://github.com/github-copilot/signup',
		description: 'Шерсть носки круто!',
		premium: true,
		sizes: ['S', 'M', 'L', 'XL', 'XXL', 'XXXL'],
    details: ['80% cotton', '20% polyester', 'Gender-neutral'],
    variants: [
      {
        variantId: 2234,
        variantColor: 'green',
        variantImage: 'https://www.vuemastery.com/images/challenges/vmSocks-green-onWhite.jpg',
        variantQuantity: 10
      },
      {
        variantId: 2235,
        variantColor: 'blue',
        variantImage: 'https://www.vuemastery.com/images/challenges/vmSocks-blue-onWhite.jpg',
        variantQuantity: 0
      }
    ],
    cart: 0,
		}
  },
  methods: {
    addToCart() {
      this.cart += 1;
    },
		MinCart() {
			if (this.cart != 0) this.cart -= 1;
		},
    updateProduct(index) {
      this.selectedVariant = index;
      console.log(index);
    }
  },
		shipping() {
			if (this.premium) {
				return "Free";
			} else {
				return '2.99';
			}
	},
  computed: {
    title() {
      return this.brand + ' ' + this.product;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock(){
      return this.variants[this.selectedVariant].variantQuantity
    },
		sale() {
			if (this.onSale) {
				return this.brand + ' ' + this.product + ' are on sale!'
			} 
				return  this.brand + ' ' + this.product + ' are not on sale'
		}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
    font-family: tahoma;
    color:#282828;
    margin: 0px;
  }
  
	.outOfStock {
  text-decoration: line-through;
	}

  .nav-bar {
    background: linear-gradient(-90deg, #84CF6A, #16C0B0);
    height: 60px;
    margin-bottom: 15px;
  }

  .product {
    display: flex;
    flex-flow: wrap;
    padding: 1rem;
  }

  img {
    border: 1px solid #d8d8d8;
    width: 80%;
    margin: 40px;
    box-shadow: 0px .5px 1px #d8d8d8;
  }
  
  .product-image {
    width: 90%;
  }
  
  .product-image,
  .product-info {
    margin-top: 10px;
    width: 50%;
  }
  
  .color-box {
    width: 40px;
    height: 40px;
    margin-top: 5px;
  }
  
  .cart {
    margin-right: 25px;
    float: right;
    border: 1px solid #d8d8d8;
    padding: 5px 20px;
  }
  
  button {
    margin-top: 30px;
    border: none;
    background-color: #1E95EA;
    color: white;
    height: 40px;
    width: 100px;
    font-size: 14px;
  } 
  .delete {
		margin-left: 10px;
	}

  .disabledButton {
    background-color: #d8d8d8;
  }
  
  .review-form {
    width: 400px;
    padding: 20px;
    margin: 40px;
    border: 1px solid #d8d8d8;
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

  .tab {
    margin-left: 20px;
    cursor: pointer;
  }

  .activeTab {
    color: #16C0B0;
    text-decoration: underline;
  }
</style>