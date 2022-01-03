<template>
    <div>

    <Header></Header>

    <div class="container">
        <h2 class="text-uppercase mb-3 mt-3" v-text="title"></h2>
        <Movies></Movies>
    </div>

    </div>
</template>

<script>
    import Movies from './Movies.vue';
    import Header from './Header.vue';

    export default {
        components: {
            Movies,
            Header
        },
        data() {
           return {
               title: "Most Popular Movies",
           }
        }
    }
</script>