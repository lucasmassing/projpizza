<template>
    <div>
        <p>{{ msg }}</p>
    </div>
</template>

<script>
export default {
    name:"Message",
    props:{
        msg:String
    }
}
</script>

<style scoped>
div {
    width: 100%;
}

p {
    max-width: 920px;
    margin: 0 auto 22px;
    padding: 14px 18px;
    border-radius: 14px;
    background: #fef3c7;
    border: 1px solid #f59e0b;
    color: #7c2d12;
    font-weight: 700;
    text-align: center;
    box-shadow: 0 10px 20px rgba(245, 158, 11, 0.12);
}
</style>