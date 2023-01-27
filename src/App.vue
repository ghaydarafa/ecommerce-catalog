<template>
  <div id="app">
    <div v-if="isLoading" class="load">
      <div class="loader"></div>
      <p>Please wait..</p>
    </div>
    <ProductDisplay
      v-show="isLoaded"
      :title="product.title"
      :image="product.image"
      :category="product.category"
      :description="product.description"
      :price="product.price"
      :men="men"
      :women="women"
      :unavailable="unavailable"
    />
  </div>
</template>

<script>
import ProductDisplay from "./components/ProductDisplay.vue";

export default {
  name: "App",
  components: {
    ProductDisplay,
  },
  data() {
    return {
      index: 1,
      product: "",
      men: false,
      women: false,
      unavailable: false,
      isLoading: false,
      isLoaded: false,
    };
  },
  methods: {
    loaded() {
      this.isLoading = false;
      this.isLoaded = true;
    },

    async getProduct() {
      try {
        this.isLoading = true;
        this.isLoaded = false;
        let response = await fetch(
          "https://fakestoreapi.com/products/" + this.index
        );
        this.product = await response.json();
        if (this.product.category == "men's clothing") {
          this.men = true;
          document.body.className = "men";
        } else if (this.product.category == "women's clothing") {
          this.women = true;
          document.body.className = "women";
        } else {
          this.unavailable = true;
          document.body.className = "unavailable";
        }
        this.loaded();
      } catch (error) {
        console.log(error);
      }
    },

    next() {
      this.men = false;
      this.women = false;
      this.unavailable = false;
      this.index += 1;
      if (this.index == 21) {
        this.index = 1;
      }
      this.getProduct();
    },
  },
  mounted() {
    this.getProduct();
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Inter");

#app {
  font-family: "Inter";
  font-style: normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  align-items: center;
  margin: 5% auto;
}

body {
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-position: center;
}

.load {
  margin-top: 20%;
}

.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #3498db; /* Blue */
  border-radius: 50%;
  display: inline-block;
  width: 40px;
  height: 40px;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
