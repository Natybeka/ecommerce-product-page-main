<template>
  <Header
    :cart="cart"
    :cartFilled="cart.length > 0 ? true : false"
    @delete-from-cart="deleteItem"
  />
  <Content :item="item" @add-to-cart="addItem" />
</template>

<script>
import Header from "./components/Header.vue";
import Content from "./components/Content.vue";
import { v4 as uuidv4 } from "uuid";

export default {
  name: "App",
  components: {
    Header,
    Content,
  },
  data() {
    return {
      item: {
        id: uuidv4(),
        name: "Autumn Limited Edition",
        price: 125.0,
        orderAmount: 0,
      },
      cart: [],
    };
  },
  methods: {
    addItem(amount, id) {
      this.item.orderAmount = amount;

      this.cart.push();
      if (this.cart.filter((item) => item.id === id).length > 0) {
        this.cart = this.cart.filter((item) => {
          if (item.id === id) {
            console.log("code here");
            item.orderAmount = amount;
          }
          return item;
        });
      } else this.cart.push(this.item);
    },

    deleteItem(id) {
      this.cart = this.cart.filter((item) => item.id !== id);
    },
  },
};
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
}
/**
* Custom color values
*/
:root {
  --primary-orange: hsl(26, 100%, 55%);
  --primary-pale-orange: hsl(25, 100%, 94%);

  --neutral-very-dark-blue: hsl(220, 13%, 13%);
  --neutral-dark-grayish-blue: hsl(219, 9%, 45%);
  --neutral-grayish-blue: hsl(220, 14%, 75%);
  --neutral-light-grayish-blue: hsl(223, 64%, 98%);
  --neutral-white: hsl(0, 0%, 100%);
  --neutral-black: hsl(0, 0%, 0%);
}

body {
  margin: 0;
  font-family: "Kumbh Sans", sans-serif;
  line-height: 1.5;
}

h1,
strong,
input {
  font-weight: 700;
}

p {
  margin: 0;
}

li {
  padding-left: 0;
  margin: 0;
}

a {
  text-decoration: none;
  color: inherit;
}

img {
  width: 100%;
  max-width: 100%;
}

#app {
  color: var(--neutral-black);
  margin: 0;
  font-size: 1rem;
}

.container {
  width: 90%;
  max-width: 1000px;
  margin: 0 auto;
}

.btn {
  display: inline-block;
  width: 100%;
  padding: 1em 2em;
  font-family: inherit;
  font-weight: 700;
  border-radius: 10px;
  border: none;
  cursor: pointer;
}

.btn-submit {
  background: var(--primary-orange);
  color: var(--neutral-white);
  flex-grow: 1;
  width: 150px;
}

.btn-submit:hover {
  opacity: 0.6;
  box-shadow: 0 10px 15px var(--primary-pale-orange);
}

input {
  font-family: inherit;
}

input:focus {
  outline: none;
}

input[type="number"] {
  -moz-appearance: textfield;
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  appearance: none;
  opacity: 0;
}

.w-75 {
  width: 85%;
}

@media (max-width: 775px) {
  .container {
    width: 100%;
  }
}
</style>
