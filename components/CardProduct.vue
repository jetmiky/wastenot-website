<template>
  <v-card>
    <v-container>
      <v-row class="align-center">
        <v-col cols="3" md="2" lg="2">
          <v-img :src="product.productImage[0]" />
        </v-col>

        <v-col cols="9" md="5" lg="5" class="px-3">
          <p class="mb-0 custom-secondary--text text-body-1 text-md-h4 text-lg-h4 font-weight-bold">
            {{ product.name }}
          </p>
          <span class="custom-primary--text text-body-2 text-md-h4 text-lg-h4 font-weight-bold">
            {{ 'Rp. ' + currency(product.price) }}
          </span>
          <p class="mt-1 text-caption hidden-xs-only">
            {{ product.description }}
          </p>
        </v-col>

        <v-col
          v-for="market in product.marketplaces"
          :key="market.name"
          cols="4"
          sm="1"
          md="1"
          lg="1"
          class="px-3 py-0"
        >
          <router-link
            :to="market.url"
            :class="market.name.toLowerCase() + '-icon'"
            class="text-caption"
          >
            {{ 'Link ' + market.name }}
          </router-link>
        </v-col>

        <v-col
          v-for="remainder in (3-countProductLink)"
          :key="remainder"
          cols="4"
          sm="1"
          md="1"
          lg="1"
        >
          <v-spacer />
        </v-col>

        <v-col cols="12" sm="2" md="2" lg="2">
          <v-btn
            class="mr-3 custom-primary--text"
            small
            :to="{
              name: 'edit-product',
              params: {
                id: product.id
              }
            }"
          >
            Edit
          </v-btn>
          <v-btn color="red darken-1" small dark @click="$emit('open-dialog')">
            Delete
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      default () {
        return {
          id: '',
          name: '',
          price: 0,
          description: '',
          productImage: [],
          marketplaces: []
        }
      }
    }
  },
  computed: {
    countProductLink () {
      return this.product.marketplaces.length
    }
  },
  methods: {
    currency (value) {
      return Intl.NumberFormat('en-US').format(value)
    }
  }
}
</script>

<style>
.shopee {
  background-color: #EE4D2D !important;
}

.shopee-icon {
  color: #EE4D2D !important;
}

.tokopedia {
  background-color: #00A600 !important;
}

.tokopedia-icon {
  color: #00A600 !important;
}

.lazada {
  background-color: #154DC5 !important;
}

.lazada-icon {
  color: #154DC5 !important;
}
</style>
