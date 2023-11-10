<script setup lang="ts"></script>

<template>
  <header class="d-flex flex-row align-items-center">
    <a href="#">
      <img src="../assets/logo.svg" alt="logo" />
      <span class="logo">Laurent</span>
    </a>
    <ul class="d-flex flex-row flex-fill">
      <li class="boutique">
        <a href="#">Boutique</a>
      </li>
      <li>
        <a href="#">Admin</a>
      </li>
    </ul>
    <ul class="ul-log-sign d-flex flex-row">
      <li class="connexion">
        <a href="#">Connexion</a>
      </li>
      <li>
        <a href="#">Inscription</a>
      </li>
    </ul>
  </header>
</template>

<style scoped lang="scss ">
header{
  background-color: var(--primary-1);
  a{
    color:var(--text-primary-color);
    display: flex;
    flex-direction: row;
    align-items: center;
    img{
      width: 20px;
      margin-right: 5px;
    }
    .logo{
      font-weight: 700;
      margin-right: 10px;
    }
  }
  ul{
    .boutique{
      margin-right: 10px;
    }
  }
  ul{
    li{

      margin-right: 10px;
    }
  }
}
</style>
