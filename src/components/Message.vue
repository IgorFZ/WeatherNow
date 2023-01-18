<template>
    <div class="message-container">
        <p> {{ msg }} </p>
    </div>
</template>

<script>
export default {
    name: "Message",
    props: {
        msg: String
    }
}
</script>

<style scoped>
    .message-container {
        color: #af233a;
        background-color: #f9e1e5;
        border: 2px solid #af233a;
        border-radius: 5px;
        padding: 20x;
        max-width: 400px;
        margin: 15px auto;
        text-align: center;
    }
    .message-container p {
        margin-bottom: 0rem;
    }
</style>