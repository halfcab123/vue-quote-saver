<template>
        <div @click="$bus.$emit('delete-quote', quote)" class="card text-dark bg-light quote">
            <div class="card-header">Quote #{{ index + 1}}</div>
            <div class="card-body">
                <div class="card-text">
                    <slot></slot>
                </div>
            </div>
        </div>
</template>

<script>
    export default {
        props: ['quote','index']
    }
</script>

<style>
    .card-text {
        font-family: 'Arizonia', cursive;
        font-size: 24px;
    }

    .quote {
        cursor: pointer;
        -webkit-transition: all 0.25s; /* For Safari 3.1 to 6.0 */
        transition: all 0.25s;
    }

    .quote:hover {
        background-color: #ffe2e2 !important;
        opacity: 0.5;
    }

    .quote:hover:before {
        position: absolute;
        font-size: 1em;
        font-family: "Arial";
        content: "X";
        top: 10px;
        right: 25px;
    }
</style>
