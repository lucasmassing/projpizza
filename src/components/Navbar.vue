<template>
    <div id="nav">
        <router-link to="/" id="logo-url">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>
        <router-link to="/">Home</router-link>   
        <router-link to="/pedidos">Pedidos</router-link>

    </div>
</template>

<script>
    export default {
       name: "Navbar" ,
       props:["logo", "alt"]
    }
</script>

<style scoped>
  #nav {
    position: sticky;
    top: 0;
    z-index: 20;
    background: rgba(34, 34, 34, 0.9);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(255, 255, 255, 0.08);
    padding: 16px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    box-shadow: 0 10px 24px rgba(0, 0, 0, 0.16);
  }

  #nav #logo-url {
    margin: auto;
    margin-left: 0;
  }

  #logo {
    width: 40px;
    height: 40px;
  }

  #nav a {
    color: #f3bf4d;
    text-decoration: none;
    margin: 12px;
    font-weight: 700;
    letter-spacing: 0.02em;
    transition: .5s;
  }

  #nav a:hover {
    color: #FFF;
  }

  @media (max-width: 700px) {
    #nav {
      padding: 14px 18px;
      gap: 8px;
      flex-wrap: wrap;
    }

    #nav a {
      margin: 6px 10px;
    }
  }
</style>
