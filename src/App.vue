<template>
  <div>
    <Navbar :logo="logo_src" :alt="app_name"/>
    <router-view/>
    <Footer/>
  </div>
  
</template>

<script>

  import Navbar from './components/Navbar.vue';
  import Footer from './components/Footer.vue';
  export default {
    components:{
      Navbar,
      Footer
    },
    data(){
      return{
        logo_src:"/img/logo.png",
        app_name:"Nossa pizza"
      }
    }
  }
</script>

<style>
  :root {
    --bg: #f4efe7;
    --surface: #ffffff;
    --surface-soft: #fff8ef;
    --text: #221b16;
    --muted: #6b5d50;
    --brand: #d97706;
    --brand-dark: #9a4f00;
    --line: #eadbc8;
    --shadow: 0 18px 40px rgba(58, 35, 10, 0.12);
    --radius-lg: 24px;
    --radius-md: 16px;
  }

  * {
    font-family: 'Trebuchet MS', 'Segoe UI', sans-serif;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  body {
    background:
      radial-gradient(circle at top left, rgba(217, 119, 6, 0.14), transparent 28%),
      radial-gradient(circle at top right, rgba(185, 28, 28, 0.08), transparent 24%),
      var(--bg);
    color: var(--text);
  }

  a {
    color: inherit;
  }

  .main-container {
    width: min(1180px, calc(100% - 32px));
    margin: 32px auto 56px;
    min-height: 250px;
  }

  h1 {
    text-align: center;
    font-size: clamp(2rem, 3vw, 3rem);
    margin-bottom: 28px;
    color: var(--text);
    letter-spacing: -0.03em;
  }

  .content-card {
    background: rgba(255, 255, 255, 0.86);
    border: 1px solid rgba(234, 219, 200, 0.9);
    box-shadow: var(--shadow);
    border-radius: var(--radius-lg);
    backdrop-filter: blur(10px);
  }

  .section-title {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
    margin-bottom: 28px;
  }

  .section-title::before,
  .section-title::after {
    content: '';
    height: 1px;
    flex: 1;
    max-width: 120px;
    background: linear-gradient(90deg, transparent, rgba(154, 79, 0, 0.35), transparent);
  }
</style>
