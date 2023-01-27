<template>
  <div class="container" :class="{ unavailable: unavailable }">
    <div class="card">
      <div v-if="men || women" class="row">
        <div class="column" id="image">
          <div class="container-img">
            <img class="product-img" :src="image" />
          </div>
        </div>
        <div class="column" id="desc">
          <div class="container-desc">
            <div class="container-title">
              <p
                class="full-title"
                :style="'visibility:' + visibility_title"
                @mouseover="visibility_title = 'visible'"
                @mouseleave="visibility_title = 'hidden'"
              >
                {{ title }}
              </p>

              <h1
                class="title"
                :class="{ men: men, women: women }"
                @mouseover="visibility_title = 'visible'"
                @mouseleave="visibility_title = 'hidden'"
              >
                {{ title }}
              </h1>
            </div>
            <table class="table-detail">
              <tr>
                <th class="detail-category">
                  {{ category }}
                </th>
                <th></th>
                <th class="score" :class="{ men: men, women: women }">
                  2.9/5
                  <span class="dot" :class="{ men: men, women: women }"></span>
                  <span class="dot" :class="{ men: men, women: women }"></span>
                  <span class="dot" :class="{ men: men, women: women }"></span>
                  <span
                    class="dot blank"
                    :class="{ men: men, women: women }"
                  ></span>
                  <span
                    class="dot blank"
                    :class="{ men: men, women: women }"
                  ></span>
                </th>
              </tr>
            </table>

            <hr />

            <div class="container-description">
              <p
                class="full-description"
                :style="'visibility:' + visibility_desc"
                @mouseenter="visibility_desc = 'visible'"
                @mouseleave="visibility_desc = 'hidden'"
              >
                {{ description }}
              </p>
              <p
                class="description"
                @mouseenter="visibility_desc = 'visible'"
                @mouseleave="visibility_desc = 'hidden'"
              >
                {{ description }}
              </p>
            </div>

            <hr />

            <h1 class="price" :class="{ men: men, women: women }">
              ${{ price }}
            </h1>

            <table class="button-section">
              <tr>
                <th class="buy-cell">
                  <button
                    class="buy-button"
                    :class="{ men: men, women: women }"
                  >
                    Buy now
                  </button>
                </th>
                <th class="next-cell">
                  <button
                    class="next-button"
                    :class="{ men: men, women: women }"
                    @click="next"
                  >
                    Next product
                  </button>
                </th>
              </tr>
            </table>
          </div>
        </div>
      </div>
      <div v-else class="content-unavailable">
        <p :class="{ unavailable: unavailable }">
          This product is unavailable to show
        </p>
        <button
          class="next-button"
          :class="{ unavailable: unavailable }"
          @click="next"
        >
          Next product
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ProductDisplay",
  props: {
    title: String,
    image: String,
    category: String,
    description: String,
    price: Number,
    men: Boolean,
    women: Boolean,
    unavailable: Boolean,
  },
  data() {
    return {
      visibility_title: "hidden",
      visibility_desc: "hidden",
    };
  },
  methods: {
    next() {
      this.$parent.next();
    },
  },
};
</script>

<style scoped>
@import url(@/assets/style/men.css);
@import url(@/assets/style/women.css);
@import url(@/assets/style/unavailable.css);

:root {
  --description-font-color: #1e1e1e;
  --category-font-color: #3f3f3f;
}

.container {
  align-items: center;
  width: 900px;
  height: 506px;
  padding: 30px;
  border-radius: 25px;
  margin-left: auto;
  margin-right: auto;
  background: white;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
}

.container.unavailable {
  background-image: url(@/assets/sad-face.png);
  background-repeat: no-repeat;
  background-attachment: scroll;
  background-position: center;
}

.card {
  text-align: center;
}

.product-img {
  width: 254px;
  height: 345px;
  margin-top: 25%;
}

.container-img {
  text-align: center;
  align-items: center;
  height: 506px;

}

.column {
  float: left;
  align-items: center;
  height: 506px;
}

#image {
  width: 40%;
}

#desc {
  width: 60%;
}

.container-desc {
  padding: 0 5%;
}

.title {
  text-align: left;
  font-family: "Inter";
  font-style: normal;
  font-weight: 600;
  font-size: 26px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2; /* number of lines to show */
  line-clamp: 2;
  -webkit-box-orient: vertical;
}

.full-title {
  margin-top: 3%;
  text-align: left;
  font-family: "Inter";
  font-style: normal;
  font-weight: 200;
  font-size: 15px;
  position: absolute;
  padding: 10px;
  border-radius: 2px;
  background: white;
  color: black;
  box-shadow: 0px 0px 6px black;
}

table {
  padding: 0;
  width: 100%;
}

.detail-category {
  text-align: left;
  font-family: "Inter";
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  color: var(--category-font-color);
}

.score {
  text-align: right;
  font-weight: 400;
  font-size: 16px;
  align-items: center;
}

.dot {
  width: 18px;
  height: 18px;
  border-radius: 50%;
  display: inline-block;
  margin-left: 2px;
}

hr {
  border: 1px solid rgba(0, 0, 0, 0.2);
}

.container-description {
  position: static;
  height: 240px;
}

.description {
  text-align: left;
  font-family: "Inter";
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  color: var(--description-font-color);
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 10; /* number of lines to show */
  line-clamp: 10;
  -webkit-box-orient: vertical;
}

.full-description {
  margin-top: 3%;
  text-align: left;
  font-family: "Inter";
  font-style: normal;
  font-weight: 200;
  font-size: 14px;
  position: absolute;
  padding: 10px;
  border-radius: 2px;
  background: white;
  color: black;
  box-shadow: 0px 0px 6px black;
}

.price {
  text-align: left;
  font-family: "Inter";
  font-style: normal;
  font-weight: 600;
  font-size: 26px;
  line-height: 34px;
}

button {
  width: 221px;
  height: 36px;
  margin: 0;
  transition-duration: 0.2s;
}

.buy-cell {
  text-align: left;
}

.next-cell {
  text-align: end;
}

.buy-button {
  border: none;
  border-radius: 4px;
  font-family: "Inter";
  font-style: normal;
  font-weight: 600;
  font-size: 18px;
  color: white;
}

.next-button {
  border-radius: 4px;
  font-family: "Inter";
  font-style: normal;
  font-weight: 600;
  font-size: 18px;
}

button.unavailable {
  width: 465px;
  height: 42px;
}
</style>
