<template>
    <div id="main-banner" :style="bannerStyle">        
    </div>
</template>

<script>
    export default{
        name: "Banner",
        computed: {
            bannerStyle() {
                return {
                    backgroundImage:
                        "linear-gradient(135deg, rgba(17, 17, 17, 0.38), rgba(17, 17, 17, 0.1)), url('/img/pizza.jpg')"
                }
            }
        }
    }
</script>

<style scoped>
   #main-banner {
        position: relative;
        overflow: hidden;
        background-position: center;
    background-size: cover;
        height: 420px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
        border-bottom: 1px solid rgba(255, 255, 255, 0.22);
        box-shadow: inset 0 -70px 80px rgba(0, 0, 0, 0.18);
    }

    #main-banner::after {
        content: '';
        position: absolute;
        inset: 0;
        background:
            linear-gradient(90deg, rgba(0, 0, 0, 0.28), transparent 48%),
            linear-gradient(0deg, rgba(0, 0, 0, 0.18), transparent 65%);
        pointer-events: none;
  }

</style>
