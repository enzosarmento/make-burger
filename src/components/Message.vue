<template>
    <div class="message-container">
        <p>
            {{ msg }}
        </p>
    </div>
</template>

<script>
export default {
    name: 'Message',
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .message-container {
        color: #004085;
        background-color: #CCE5FF;
        border: 2px solid #B8DAFF;
        border-radius: 3px;
        max-width: 400px;
        height: 3.5rem;
        margin: 1.875rem auto;

        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>