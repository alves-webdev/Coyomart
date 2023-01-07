<template>
  <nav>
    <h1>Coyo Mart</h1>
    <router-link to="/" class="nav-link">Home</router-link>
    <router-link to="/users" class="nav-link">Usuarios</router-link>
    <router-link to="/products" class="nav-link">Produto</router-link>
  </nav>
</template>

<style>
  nav {
    display: flex;
    flex-direction: column;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    gap: 16px;
    bottom: 0;
    width: 300px;
    background-color: #244474;
  }

  h1 {
    padding: 16px;
    font-size: 24px;
    color: #fff;
  }

  .nav-link {
    display: block;
    padding: 16px;
    font-size: 20px;
    text-decoration: none;
    color: #ffffff;
    width: 80%;
    border-radius: 10px;
    background-color: #182d4d;
    text-align: center;
    transform: scale(1);
    transition: ease-in-out 0.5s;
    font-weight: bold;
    font-family: 'Roboto', sans-serif;
  }

  .nav-link:hover,
  .nav-link.router-link-active {
    color: #182d4d;
    transform: scale(1.11);
    background-color: #fff;
    border-radius: 0px;
  }
</style>
