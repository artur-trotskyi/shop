<template>
  <!-- Prodcuts -->
  <section :class="itemView">
    <b-card
      v-for="product in products"
      :key="product.id"
      class="ecommerce-card"
      no-body
    >
      <div class="item-img text-center">
        <b-link :to="{ name: 'apps-e-commerce-product-details', params: { slug: product.slug } }">
          <b-img
            :alt="`${product.name}-${product.id}`"
            fluid
            class="card-img-top"
            :src="product.image"
          />
        </b-link>
      </div>

      <!-- Product Details -->
      <b-card-body>
        <div class="item-wrapper">
          <div class="item-rating">
            <ul class="unstyled-list list-inline">
              <li
                v-for="star in 5"
                :key="star"
                class="ratings-list-item"
                :class="{'ml-25': star-1}"
              >
                <feather-icon
                  icon="StarIcon"
                  size="16"
                  :class="[{'fill-current': star <= product.rating}, star <= product.rating ? 'text-warning' : 'text-muted']"
                />
              </li>
            </ul>
          </div>
          <div>
            <h6 class="item-price">
              ${{ product.price }}
            </h6>
          </div>
        </div>
        <h6 class="item-name">
          <b-link
            class="text-body"
            :to="{ name: 'apps-e-commerce-product-details', params: { slug: product.slug } }"
          >
            {{ product.name }}
          </b-link>
          <b-card-text class="item-company">
            By
            <b-link class="ml-25">
              {{ product.brand }}
            </b-link>
          </b-card-text>
        </h6>
        <b-card-text class="item-description">
          {{ product.description }}
        </b-card-text>
      </b-card-body>

      <!-- Product Actions -->
<!--      <div class="item-options text-center">
        <div class="item-wrapper">
          <div class="item-cost">
            <h4 class="item-price">
              ${{ product.price }}
            </h4>
          </div>
        </div>
        <b-button
          variant="light"
          tag="a"
          class="btn-wishlist"
          @click="toggleProductInWishlist(product)"
        >
          <feather-icon
            icon="HeartIcon"
            class="mr-50"
            :class="{'text-danger': product.isInWishlist}"
          />
          <span>Wishlist</span>
        </b-button>
        <b-button
          variant="primary"
          tag="a"
          class="btn-cart"
          @click="handleCartActionClick(product)"
        >
          <feather-icon
            icon="ShoppingCartIcon"
            class="mr-50"
          />
          <span>{{ product.isInCart ? 'View In Cart' : 'Add to Cart' }}</span>
        </b-button>
      </div>-->
    </b-card>
  </section>
</template>

<script>
import {
  BDropdown,
  BDropdownItem,
  BFormRadioGroup,
  BFormRadio,
  BRow,
  BCol,
  BInputGroup,
  BInputGroupAppend,
  BFormInput,
  BCard,
  BCardBody,
  BLink,
  BImg,
  BCardText,
  BButton,
  BPagination,
} from 'bootstrap-vue'
import Ripple from 'vue-ripple-directive'
import axios from 'axios'
import { useShopUi } from './useECommerceShop'

export default {
  name: 'ECommerceShop',
  directives: {
    Ripple,
  },
  components: {
    // BSV
    BDropdown,
    BDropdownItem,
    BFormRadioGroup,
    BFormRadio,
    BRow,
    BCol,
    BInputGroup,
    BInputGroupAppend,
    BFormInput,
    BCard,
    BCardBody,
    BLink,
    BImg,
    BCardText,
    BButton,
    BPagination,

    // SFC
    // ShopLeftFilterSidebar,
  },
  data() {
    return {
      products: [],
    }
  },
  created() {
    axios
      .get('http://shop.localhost/api/products')
      .then(response => {
        this.products = response.data
        console.log(this.products)
      })
  },
  setup() {
    const {
      itemView,
    } = useShopUi()

    return {
      itemView,
    }
  },
}
</script>

<style lang="scss">
@import "~@core/scss/base/pages/app-ecommerce.scss";
</style>

<style lang="scss" scoped>
.item-view-radio-group ::v-deep {
  .btn {
    display: flex;
    align-items: center;
  }
}
</style>
