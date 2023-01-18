<script setup>
  import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <nav aria-label="breadcrumb">
      <ol class="breadcrumb">
        <li class="breadcrumb-item">
            <RouterLink to="/">Home</RouterLink>
        </li>
        <li class="breadcrumb-item">
            <RouterLink to="/about">About</RouterLink>
        </li>
      </ol>
    </nav>
  </div>
</nav>
</template>

<script>
export default {
    name: "Navbar"
}
</script>