<template>
  <div class="app">
    <main>
      <div v-if="loading" class="loader"></div>
      <div class="outer-wrapper">
        <div
          v-if="!isUnavailableProduct && !loading"
          class="product-container"
          :class="{ 'men-section': isMenSection, 'women-section': isWomenSection }"
          :style="{ height: isMenSection || isWomenSection ? '500px' : 'auto' }"
        >
          <div class="product">
            <img :src="product.image" :alt="product.title" class="product-image">
            <div class="product-details">
              <h2 :style="{ color: isMenSection ? colorPalette.blue : isWomenSection ? colorPalette.pink : 'grey' }">{{ product.title }}</h2>
              <p :style="{ color: isMenSection ? colorPalette.blue : isWomenSection ? colorPalette.pink : 'grey' }">{{ product.category }}</p>
              <hr>
              <p>{{ product.description }}</p>
              <hr>
              <b><p class="harga" :style="{ color: isMenSection ? colorPalette.blue : isWomenSection ? colorPalette.pink : 'grey' }">Price: ${{ product.price }}</p></b>
              <div class="button-container">
                <button class="next" @click="getNextProduct">Next Product</button>
                <button class="buy-button">Buy Now</button>
              </div>
            </div>
          </div>
        </div>
        <div v-else-if="isUnavailableProduct && !loading" class="unavailable-wrapper">
          <div class="unavailable-product">
            <img src="@/assets/images/unavailable.jpg" alt="Unavailable" class="unavailable-image">
            <h2>This product is unavailable to show</h2>
            <button class="nextt" @click="getNextProduct">Next Product</button>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: {},
      currentIndex: 1,
      isMenSection: false,
      isWomenSection: false,
      isUnavailableProduct: false,
      loading: false,
      colorPalette: {
        blue: '#002772',
        pink: '#720060',
      },
    };
  },
  methods: {
    async getNextProduct() {
      this.loading = true; 
      try {
        const response = await fetch(`https://fakestoreapi.com/products/${this.currentIndex}`);
        const data = await response.json();
        if (data.category === "men's clothing") {
          this.isMenSection = true;
          this.isWomenSection = false;
          this.isUnavailableProduct = false;
        } else if (data.category === "women's clothing") {
          this.isMenSection = false;
          this.isWomenSection = true;
          this.isUnavailableProduct = false;
        } else {
          this.isMenSection = false;
          this.isWomenSection = false;
          this.isUnavailableProduct = true;
        }
        this.product = data;
        this.currentIndex = (this.currentIndex % 20) + 1;
      } catch (error) {
        console.error('Error fetching data:', error);
      }
      this.loading = false; 
    },
  },
};

</script>
