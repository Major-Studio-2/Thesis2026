<script>
export default {
  name: "ShoppingBlock",
  props: {
    itemPrice: Number,
    itemCount: Number,
    imageUrl: String,
  },
  emits: ["add", "remove"],
};
</script>

<template>
  <div class="container">
    <div>
      <div class="image-container"><img :src="imageUrl" /></div>

      <div>Price: ${{ itemPrice }}.00</div>
    </div>

    <div>
      <button @click="$emit('add')">Add</button>
      <button @click="$emit('remove')">Remove</button>
      <br />
      <div>Items: {{ itemCount }}</div>
    </div>
  </div>
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
