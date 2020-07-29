<template>
    <div id="myModal" class="modal">

        <!-- Modal content -->
        <div class="modal-content">
            <div class="modal-header"><h3>Oops</h3><div class="close" @click="onClose()">&times;</div></div>
            <p v-html="message"></p>
        </div>

    </div>

</template>

<script>
    export default {
        name: "Modal",
        props: {
            onClose: {type: Function},
            message: {type: String}
        }
    }
</script>

<style scoped lang="scss">
    @import "../../scss/index";
    /* The Modal (background) */
    .modal {
        /*display: none; !* Hidden by default *!*/
        position: fixed; /* Stay in place */
        z-index: 1; /* Sit on top */
        left: 0;
        top: 0;
        width: 100%; /* Full width */
        height: 100%; /* Full height */
        overflow: auto; /* Enable scroll if needed */
        background-color: rgb(0,0,0); /* Fallback color */
        background-color: rgba(0,0,0,0.4); /* Black w/ opacity */

        /* Modal Content/Box */
        .modal-content {
            background-color: $modal-content-background-color;
            margin: 15% auto; /* 15% from the top and centered */
            border-radius: 6px;
            width: 60%; /* Could be more or less, depending on screen size */
            .modal-header {
                border-radius: 6px 6px 0px 0px;
                padding: 10px 20px 0px 20px;
                background-color: $error-color;
                color:$white;
                display: flex;
                flex-direction: row;
                justify-content: space-between;
            }
            p {
                padding-left: 20px;
                padding-top: 10px;
                min-height: 80px;
            }
        }

        /* The Close Button */
        .close {
            font-size: 1.2em;
            font-weight: bold;
        }

        .close:hover,
        .close:focus {
            color: black;
            text-decoration: none;
            cursor: pointer;
        }
    }


</style>
