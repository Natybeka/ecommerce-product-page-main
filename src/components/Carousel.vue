<template>
    
    <div class="wrapper">
        <section class="carousel">
            <div class="slide"><img src="../assets/images/image-product-1.jpg" alt="product image 1" class="product-image"/></div>
            <div class="slide"><img src="../assets/images/image-product-2.jpg" alt="product image 2" class="product-image"/></div>
            <div class="slide"><img src="../assets/images/image-product-3.jpg" alt="product image 2" class="product-image"/></div>
            <div class="slide"><img src="../assets/images/image-product-4.jpg" alt="product image 2" class="product-image"/></div>
            <div @click="previousImage()" class="previous-icon">
                <img src="../assets/images/icon-previous.svg" alt="previous image" >
            </div>
            <div @click="nextImage()" class="next-icon">
                <img src="../assets/images/icon-next.svg" alt="next image">
            </div>
        </section>
        <section class="thumbnail-section">
            <img src="../assets/images/image-product-1-thumbnail.jpg" alt="product image 1 thumbnail" @click="showImage(0)" class="product-thumbnail"/>
            <img src="../assets/images/image-product-2-thumbnail.jpg" alt="product image 1 thumbnail" @click="showImage(1)" class="product-thumbnail"/>
            <img src="../assets/images/image-product-3-thumbnail.jpg" alt="product image 1 thumbnail" @click="showImage(2)" class="product-thumbnail"/>
            <img src="../assets/images/image-product-4-thumbnail.jpg" alt="product image 1 thumbnail" @click="showImage(3)" class="product-thumbnail"/>
        </section>
    </div>

</template>


<script>
export default {
    name: "carousel-component",
    mounted() {

        this.slides = document.querySelectorAll(".slide");

        

        this.allThumbnails = document.querySelectorAll('.product-thumbnail');
        
        this.allThumbnails[this.currentSlide].style.opacity = '.6';

        this.slides.forEach((slide, index) => slide.style.transform = `translateX(${index * 100}%)`);
    },
    data() {
        return {
            currentSlide : 0,
            slides : HTMLCollection,
            allThumbnails: HTMLCollection
        }
    },  
    methods: {
        showImage(index) {
            this.allThumbnails[this.currentSlide].style.opacity = '1';

            this.currentSlide = index;

            this.allThumbnails[this.currentSlide].style.opacity = '.6';

            this.slides.forEach((slide, index) => {
                slide.style.transform = `translateX(${100 * (this.currentSlide - index)}%)`;
            });



        },
        previousImage() {
            
            this.allThumbnails[this.currentSlide].style.opacity = '1';

            if (this.currentSlide === 0) {
                this.currentSlide = this.slides.length - 1;
            }
            else {
                this.currentSlide--;
            }

            this.allThumbnails[this.currentSlide].style.opacity = '.6';

            this.slides.forEach((slide, index) => {
                slide.style.transform = `translateX(${100 * (this.currentSlide - index)}%)`;
            });
        },

        nextImage() {
            
            this.allThumbnails[this.currentSlide].style.opacity = '1';
            if (this.currentSlide === this.slides.length - 1) {
                this.currentSlide = 0;
            }
            else {
                this.currentSlide++;
            }

            this.allThumbnails[this.currentSlide].style.opacity = '.6';

            
            this.slides.forEach((slide, index) => {
                slide.style.transform = `translateX(${100 * (index - this.currentSlide)}%)`;
            });
        }
    }
}
</script>


<style scoped>

.carousel {
    position: relative;
    height: 380px;
    width: 100%;
    overflow: hidden;
    
}
.thumbnail-section {
    display: none;
}

.product-thumbnail  {
    width: 22%;
    border-radius: 15px;
}

.slide  {
    width: 100%;
    height: 100%;
    position: absolute;
    transition: all .5s;
}

.slide img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.previous-icon, .next-icon {
    position: absolute;
    top: 45%;
    width: 28px;
    height: 28px;
    background: var(--neutral-white);
    border-radius: 50%;
}

.previous-icon img, .next-icon img {
    position: absolute;
    object-fit: cover;
    left: 50%;
    transform: translate(-50%, 50%);
    height: 14px;
    width: 14px;
    cursor: pointer;
}

.next-icon {
    right: 0;
    margin-right: 10px;
}

.previous-icon {
    margin-left: 10px;
}
.product-image {
    width: 100%;
}

@media (min-width: 625px) {
    .slide {
        border-radius: 15px;
        overflow: hidden;
    }
    .product-image, .product-thumbnail {
        cursor: pointer;
    }

    .thumbnail-section {
        display: flex;
        margin-top: 20px;
        padding: 0 1em;
        justify-content: space-between;
    }   
  
    .previous-icon, .next-icon {
        display: none;
    }
}
</style>