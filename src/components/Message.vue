<template>
    <div class="message">
        <p> {{message}} </p>
    </div>
</template>

<script>
    export default {
        props: {
            message: {
                type: String,
                required: true,
            }
        }
    }
</script>

<style scoped>
    .message {
        margin-bottom: 15px;
        color: rgb(187, 10, 10);
        text-align: center;
    }
</style>