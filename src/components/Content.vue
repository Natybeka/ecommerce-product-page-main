<template>
    <div class="container-grid">
        <Carousel />
        <Description :id="item.id"  @add-to-cart="addToCart" />
    </div>
</template>

<script>
import Carousel from "./Carousel.vue";
import Description from './Description.vue';
export default  {
    name: "content-component",
    emits: ['add-to-cart'],
    components: {
        Carousel,
        Description
    },
    props: {
        item: Object
    },
    methods: {
        addToCart(amount, id) {
            this.$emit("add-to-cart", amount, id);
        }
    }
        
}

</script>

<style scoped>
.container-grid {
    width: 90%;
    max-width: 1000px;
    margin: 0 auto;
    display: grid;
    gap: 30px;
}

@media (max-width: 625px) {
    .container-grid {
        width: 100%;
    }
}

@media (min-width: 625px) {
    .container-grid {
        padding: 4em 2em;
    }
}

@media (min-width: 775px) {
    .container-grid {
        grid-template-columns: 1.25fr 1fr;
    }
}
</style>