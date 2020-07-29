<template>
    <div id="app" @keyup.esc="handleEscape()">
        <BookMarks/>
    </div>
</template>

<script>
    import BookMarks from './components/BookMarks.vue'
    import {EventBus} from './event-bus';

    export default {
        name: 'App',
        components: {
            BookMarks
        },
        methods: {
            handleEscape() {
                EventBus.$emit('escape-clicked')
            }
        }
    }
</script>

<style lang="scss">
    @import "scss/index";
    #app {
        background-color: $app-background-color;
        padding: 20px;
        width:60%;
        @media all and (max-width: 480px) {
            width: 90%;
        }
        margin-left: auto;
        margin-right: auto;
        margin-top: 20px;
    }


</style>
