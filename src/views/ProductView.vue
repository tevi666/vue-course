<template>
    <main>
        <div
            class="banner"
            :class="
                pageName === 'coffee' ? 'coffepage-banner' : 'goodspage-banner'
            "
        >
            <div class="container">
                <div class="row">
                    <div class="col-lg-6">
                        <navbar-component />
                    </div>
                </div>
                <header-title-component v-if="product" :title="product.name" />
            </div>
        </div>

        <section class="shop" v-if="product">
            <div class="container">
                <div class="row">
                    <div class="col-lg-5 offset-1">
                        <img
                            style="max-width: 100%"
                            class="shop__girl"
                            :src="product.image"
                            :alt="product.image"
                        />
                    </div>
                    <div class="col-lg-4">
                        <div class="title">About it</div>
                        <img
                            class="beanslogo"
                            src="@/assets/logo/Beans_logo_dark.svg"
                            alt="Beans logo"
                        />
                        <div class="shop__point" v-if="product.country">
                            <span>Country:</span>
                            {{ product.country }}
                        </div>
                        <div class="shop__point" v-if="product.description">
                            <span>Description:</span>
                            {{ product.description }}
                        </div>
                        <div class="shop__point">
                            <span>Price: </span>
                            <span class="shop__point-price">{{
                                product.price
                            }}</span>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>
</template>

<script>
import NavbarComponent from '@/components/NavbarComponent'
import HeaderTitleComponent from '@/components/HeaderTitleComponent.vue'
export default {
    components: { NavbarComponent, HeaderTitleComponent },
    data() {
        return {
            product: null,
        }
    },
    mounted() {
        fetch(`http://localhost:3000/${this.pageName}/${this.$route.params.id}`)
            .then((res) => res.json())
            .then((data) => {
                this.product = data
            })
    },
    destroyed() {
        this.product = null
    },
    computed: {
        pageName() {
            return this.$route.name
        },
        card() {
            const pageGetter =
                this.pageName === 'coffee' ? 'getCoffeeById' : 'getGoodsById'
            return this.$store.getters[pageGetter](this.$route.params.id)
        },
    },
}
</script>