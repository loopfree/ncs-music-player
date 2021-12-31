<template>
    
    <div class="container">
        <component
            :is="screens[position]"
        />
    </div>

</template>

<script>
    import songList from "./components/songList.vue";

    export default {
        components: {
            songList,
        },

        data() {
            return {
                screens: ["songList"],
                position: 0
            }
        },

        methods: {

        },
    }

</script>

<style>

    @import "~@/assets/style.css";
    
</style>