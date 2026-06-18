<template>
    <footer id="footer">
        <p>Make Your Pizza &copy; 2026</p>
    </footer>
</template>
<script>
export default {
    name:"Footer"
}
</script>

<style scoped>
  #footer {
    min-height: 160px;
    background: linear-gradient(180deg, #222, #161616);
    border-top: 1px solid rgba(255, 255, 255, 0.08);
    color: #f4c15f;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    letter-spacing: 0.04em;
    bottom: 0;
    width: 100%;
  }
</style>