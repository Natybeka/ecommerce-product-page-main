<template>
  <header class="container">
    <nav>
      <!-- Logo -->
      <div class="nav-container">
        <img
          @click="toggleNav()"
          src="../assets/images/icon-menu.svg"
          class="menu-btn"
        />

        <img
          @click="closeNav()"
          src="../assets/images/icon-close.svg"
          alt="close icon"
          class="close-btn"
        />

        <a href="#" class="logo"
          ><img src="../assets/images/logo.svg" alt="logo"
        /></a>
        <ul class="nav-list">
          <li><a href="#">Collections</a></li>
          <li><a href="#">Men</a></li>
          <li><a href="#">Women</a></li>
          <li><a href="#">About</a></li>
          <li><a href="#">Contact</a></li>
        </ul>
      </div>

      <div class="nav-aside">
        <div class="cart-icon" @click="toggleCart()">
          <img src="../assets/images/icon-cart.svg" alt="cart icon" />
          <p v-show="cartFilled" class="filled-badge">1</p>
        </div>
        <div class="cart">
          <p>Cart</p>
          <div v-if="cart.length > 0" class="cart-items">
            <div v-for="item in cart" :key="item.id" class="cart-item">
              <img
                src="../assets/images/image-product-1-thumbnail.jpg"
                class="product-image"
                alt="product thumbnail"
              />
              <p>
                {{ item.name }}<br />
                ${{ item.price }}.00 x {{ item.orderAmount }}&nbsp;<strong
                  :style="'color:black;'"
                  >${{ item.price * item.orderAmount }}</strong
                >
              </p>
              <img
                src="../assets/images/icon-delete.svg"
                class="delete-item"
                @click="deleteItem(item.id)"
                alt="delete item"
              />
            </div>

            <button class="btn btn-submit w-75">Checkout</button>
          </div>

          <div v-else :style="'text-align:center;'">
            <p style="margin-top: 20px">The cart is empty</p>
          </div>
        </div>
        <img
          src="../assets/images/image-avatar.png"
          class="profile-avatar"
          alt="profile avatar"
        />
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: "header-component",
  props: {
    cart: Array,
    cartFilled: Boolean,
  },

  emits: ["delete-from-cart"],
  methods: {
    // Methods for toggling navigations
    toggleNav() {
      console.log("toggling navigation");
      let navList = document.querySelector(".nav-list");
      navList.classList.add("nav-list-visible");

      document.querySelector(".menu-btn").classList.add("hidden");
      let closeNav = document.querySelector(".close-btn");
      closeNav.classList.add("visible");
    },

    closeNav() {
      let navList = document.querySelector(".nav-list");
      navList.classList.remove("nav-list-visible");

      document.querySelector(".menu-btn").classList.remove("hidden");
      let closeNav = document.querySelector(".close-btn");
      closeNav.classList.remove("visible");
    },

    toggleCart() {
      document.querySelector(".cart").classList.toggle("cart-visible");
    },

    deleteItem(id) {
      this.$emit("delete-from-cart", id);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
header {
  padding: 1.125em 2em;
  border-bottom: 1px solid var(--neutral-light-grayish-blue);
}
nav,
.nav-container,
.nav-aside {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
}
.nav-aside {
  gap: 15px;
  align-items: center;
}

.menu-btn,
.close-btn {
  padding: 0;
  z-index: 300;
}

.menu-btn {
  height: 15px;
  width: 20px;
}

.menu-btn.hidden {
  display: none;
}

.close-btn {
  display: none;
  width: 20px;
  height: 20px;
}

.close-btn.visible {
  display: inline-block;
}

.profile-avatar,
.menu-btn,
.logo,
.close-btn,
.cart-icon {
  cursor: pointer;
}
.profile-avatar {
  width: auto;
  height: 100%;
  margin-top: -8px;
}
.cart-icon {
  position: relative;
  min-width: 20px;
  height: 100%;
}

.filled-badge {
  color: var(--neutral-white);
  background: var(--primary-orange);
  padding: 1px 5px;
  font-size: 0.5rem;
  font-weight: 700;
  text-align: center;
  position: absolute;
  top: -3px;
  right: -3px;
  border-radius: 50%;
}

.logo {
  min-width: 100px;
}

.profile-avatar {
  height: 30px;
  object-fit: cover;
}
.profile-avatar:hover {
  border-radius: 50%;
  border: 1px solid var(--primary-orange);
}
.nav-list {
  z-index: 200;
  position: fixed;
  width: 70%;
  margin: 0;
  top: 0;
  left: -70%;
  bottom: 0;
  list-style-type: none;
  transition: transform 250ms ease-in-out;
  color: var(--neutral-dark-grayish-blue);
}

.nav-list-visible {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  padding: 5em 0 0 2em;
  transform: translateX(100%);
  background: var(--neutral-white);
  box-shadow: 30vw 0 0 rgba(0, 0, 0, 0.75);
}

.nav-list-visible li:not(:last-child) {
  margin-bottom: 20px;
}

a:hover,
a:focus {
  color: var(--primary-orange);
}

.cart {
  position: absolute;
  background: var(--neutral-white);
  box-shadow: 0 0 10px var(--neutral-black);
  left: 50%;
  transform: translate(-50%, 165px);
  width: 92vw;
  max-width: 450px;
  z-index: 600;
  border: none;
  border-radius: 5px;
  min-height: 250px;
  display: none;
}

.cart-items {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.cart-item {
  display: flex;
  justify-content: space-between;
  width: 100%;
  gap: 15px;
  align-items: center;
  padding: 0 1.5em;
  margin-top: 20px;
}

.cart-item .product-image {
  width: 50px;
  height: 100%;
  border-radius: 5px;
}

.cart-item .delete-item {
  width: 20px;
  height: 100%;
  cursor: pointer;
}

.cart-item p {
  width: 60%;
  flex-grow: 1;
  text-align: left;
  color: var(--neutral-dark-grayish-blue);
  flex-wrap: nowrap;
}

.cart > p:first-child {
  border-bottom: 2px solid var(--neutral-light-grayish-blue);
  font-weight: 700;
  padding: 1em 2em;
}

.cart-visible {
  display: block;
}

@media (min-width: 625px) {
  .nav-aside {
    position: relative;
  }
  .menu-btn {
    display: none;
  }

  header {
    padding-top: 2em;
    padding-bottom: 2em;
  }

  .nav-list {
    position: relative;
    display: flex;
    padding: 0;
    left: 0;
  }

  .nav-list li:not(:first-child) {
    margin-left: 15px;
  }

  .nav-list a {
    position: relative;
    display: block;
    transition: transform 250ms ease;
  }

  .nav-list a::after {
    content: "";
    height: 2px;
    width: 100%;
    background: var(--primary-orange);
    position: absolute;
    bottom: -38px;
    display: none;
  }

  .nav-list a:hover,
  .nav-list a:focus {
    color: black;
    outline: none;
  }

  .nav-list a:hover::after,
  .nav-list a:focus::after {
    display: block;
  }

  .cart {
    max-width: 340px;
    z-index: 300;
    transform: translate(-75%, 160px);
    /* transform: translateX(-100%); */
  }
}

@media (max-width: 775px) and (min-width: 625px) {
  .cart {
    transform: translate(-85%, 160px);
  }
}
</style>
