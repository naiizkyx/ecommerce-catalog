<!-- <template>
  <div class="app">
    <main>
      <head>
      <link rel="stylesheet" href="D:\crs\belajar\rakamin\TASK-5\ecommerce\src\assets\style\page.css">
      </head>
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

<style scoped>

.app {
  font-family: 'Times New Roman', Times, serif, sans-serif;
}

main {
  top: 0;
  padding: 0px;
  margin: auto;
}
p.harga{
  font-size: 18px;
}
.outer-wrapper {
  padding: 0 auto;
}
.product-container {
  background-color: #ffffff;
  width: 100%;
  padding: 0;
  z-index: -1;
  position: fixed;
}

.product {
  width: 70%;
  margin: 0 auto;
  margin-top:200px;
  padding: 20px;
  border-radius: 5px;
  background-color: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 0 2px #dcdcdc;
}

.product-image {
  width: 30%;
  margin-right: 20px;
}

.product-details {
  width: 70%;
}
.unavailable-wrapper {
  height: 350px;
  width: 100%;
  position: fixed;
  top: 0;
  z-index: -1;
  background-color: #dcdcdc; 
  display: flex;
  justify-content: center;
}
.unavailable-product {
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 20px;
  margin: 0 auto;
  margin-top: 200px;
  width: 70%;
  height: 120%;
  background-color: #ffffff;
  color: #333;
  border-radius: 99;
  box-shadow: 0 0 0 2px #dcdcdc;
}

.unavailable-image {
  width: 25%;
  margin-bottom: 20px;
}

.men-section {
  background-color: #D6E6FF;
  color: #000000;
}

.women-section {
  background-color: #FDE2FF;
  color: #000000;
}

button {
  font-size: medium;
  padding: 8px;
  border: solid 2px;
}

button:hover {
  background-color: #dcdcdc;
}

button.next {
  margin-right: 20px;
  background-color: transparent;
  color: #1e1e1e;
  border-color: #1e1e1e;
}

.women-section button.next {
  color: white;
  background-color: #720060;
  border-color: #720060;
}

.women-section button.next:hover {
  color: white;
  background-color: #852977;
  border-color: #720060;
}

.women-section button.buy-button {
  color: #720060;
  border-color: #720060;
}

main.men-section {
  background-color: #720060;
}

.men-section button.next {
  color: white;
  background-color: #002772;
  border-color: #002772;
}

.men-section button.next:hover {
  color: white;
  background-color: #244f9e;
  border-color: #002772;
}

.men-section button.buy-button {
  color: #002772;
  border-color: #002772;
}

.loader {
  margin: auto;
  margin-top: 400px;
  border: 16px solid #f3f3f3;
  border-top: 16px solid #3498db;
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style> -->
