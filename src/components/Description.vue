<template>
    <section class="product-description">
        <p class="brand-name">sneaker company</p>
        <h2>Fall Limited Edition Sneakers</h2>
        <p class="product-text">These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer sole, they'll withstand everything the weather can offer.</p>

        <div class="pricing">
            <h2 class="price">$125.00</h2>
            <p class="original-price">$250.00</p>
        </div>

        <form class="add-to-cart-form" @submit.prevent="submitOrder()">
            <div class="control-group">
                <div class="btn minus-btn" @click="decreaseAmount()"><img src="../assets/images/icon-minus.svg" alt="remove item"></div>
                <input type="number" class="number-of-items" v-model="orderAmount" disabled required aria-required>
                <div class="btn plus-btn" @click="increaseAmount()"><img src="../assets/images/icon-plus.svg" alt="add item" class="add-item"></div>
            </div>


            <button class="btn btn-submit" type="submit">
            <font-awesome-icon icon="fas fa-cart-shopping" />
            <span style="margin-left: 10px">Add to cart</span></button>

             <div v-show="showError" class="form-errors">
            <p>Error during input</p>
        </div>
        </form>

       
    </section>
</template>

<script>
export default {
    name: "item-description-component",
    emits: ['add-to-cart'],
    data() {
        return {
            orderAmount: 0,
            showError: false
        }
    },
    props: {
        id: String
    },
    methods: {
        submitOrder() {
            if (this.orderAmount === 0) {
                this.showError = true;
                return;
            }
            
            this.showError = false;
            this.$emit("add-to-cart", this.orderAmount, this.id);

        },
        increaseAmount() {
            this.showError = false;
            this.orderAmount++;
        },
        decreaseAmount() {
            this.showError = false;
            if (this.orderAmount === 0) {
                return;
            }
            this.orderAmount--;
        }
    }
}
</script>


<style scoped>

.brand-name {
    text-transform: uppercase;
    font-size: .75rem;
    letter-spacing: 1px;
    font-weight: 700;
    color: var(--primary-orange);    
}

.product-description {
    padding: 1.5em 1.5em;
    width: 100%;
}

.product-text {
    color: var(--neutral-dark-grayish-blue);
    margin-bottom: 20px;
}
.pricing {
    position: relative;
}

.price {
    margin: 0;
    float: left;
    position: relative;
}

.price::after {
    content: '50%';
    font-size: .75rem;
    padding: .25em .45em;
    background: var(--primary-pale-orange);
    color: var(--primary-orange);
    position: absolute;
    left: 120%;
    bottom: 15%;
}


.original-price {
    position: absolute;
    padding-right: 0;
    right: 0;
    transform: translate(0, 30%);
    text-decoration: line-through;
    color: var(--neutral-dark-grayish-blue);
}

form {
    position: relative;
    clear: both;
    padding-top: 20px;
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    gap: 5px;
}

.control-group {
    display: flex;
    width: 100%;
    align-items: center;
    justify-content: center;
    width: 150px;
    flex-grow: 1;
}

.control-group * {
    height: 45px;
    text-align: center;
    background: var(--neutral-light-grayish-blue);
}

.control-group .btn {
    width: 20%;
    position: relative;
    user-select: none;
}

.control-group input {
    width: 60%;
    text-align: center;
    border: none;
    
}

.control-group img {
    position: absolute;
    top: 50%;
    width: 15px;
    transform: translate(-50%, 0);
    height: 5px;
    object-fit: cover;
}

.plus-btn {
    border-radius: 0 10px 10px 0;
}

.minus-btn {
    border-radius: 10px 0 0 10px;
}

.form-errors {
    text-align: center;
    background: var(--primary-pale-orange);
    font-size: 1.125rem;
    color: rgb(187, 67, 67);
    position: absolute;
    width: 100%;
    margin: 0 auto;
    bottom: -45px;
    padding: .3625em 0;
    transition: display 350ms ease;
}

.control-group .add-item {
    height: 15px;
    width: 15px;
    transform: translate(0, -50%);
}

@media (min-width: 625px) {
    .price {
        float: initial;
    }
    
    .price::after {
        left: 90px;
    }

    .original-price {
        position: relative;
    }
}
</style>