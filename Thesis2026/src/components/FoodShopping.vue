<script>
import ShoppingBlock from "./ShoppingBlock.vue";
export default {
  name: "FoodShopping",
  components: {
    ShoppingBlock,
  },
  data() {
    return {
      itemPrice: [],
      itemCount: [],
      imageUrl: [],
    };
  },

  // use as functions
  methods: {
    add(idx) {
      this.itemCount[idx] += 1;
    },

    remove(idx) {
      this.itemCount[idx] -= 1;
      this.itemCount[idx] = Math.max(this.itemCount[idx], 0);
    },
  },

  // special functions that get used as if they were values.
  // automatically run/update when variables inside of them change
  computed: {
    totalPrice() {
      let sum = 0;
      for (let idx = 0; idx < this.itemPrice.length; idx++) {
        sum += this.itemCount[idx] * this.itemPrice[idx];
      }
      return sum;
    },

    totalItems() {
      let total = 0;
      for (let idx = 0; idx < this.itemCount.length; idx++) {
        total += this.itemCount[idx];
      }
      return total;
    },
  },

  async created() {
    for (let idx = 0; idx < 40; idx++) {
      this.itemPrice.push(parseInt(Math.random() * 15 + 15));
    }

    for (let idx = 0; idx < this.itemPrice.length; idx++) {
      const res = await fetch("https://foodish-api.com/api/");
      const data = await res.json();
      this.imageUrl.push(data.image);
      this.itemCount.push(0);
    }
  },
};
</script>

<template>
  <div class="total">
    <div>Total Items: {{ totalItems }}</div>
    <div>Total Price: {{ totalPrice }}</div>
  </div>

  <ShoppingBlock
    v-for="(price, index) in itemPrice"
    :key="index"
    :itemPrice="price"
    :itemCount="itemCount[index]"
    :imageUrl="imageUrl[index]"
    @add="add(index)"
    @remove="remove(index)"
  />
</template>

<style scoped>
* {
  margin: 0;
  box-sizing: border-box;
}

.container {
  display: inline-flex;
  flex-direction: row;
  max-width: 400px;
  margin: 16px;
  gap: 0 14px;
  background-color: #e0e0e0;
  padding: 24px 16px;
}

.image-container {
  width: 100px;
  height: 100px;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: fill;
}

.total {
  width: 100%;
  padding: 16px;
  font-family: sans-serif;
  font-size: 24px;
}

button {
  min-width: 80px;
  height: 30px;
  cursor: pointer;
}

button + button {
  margin-left: 4px;
}
</style>
