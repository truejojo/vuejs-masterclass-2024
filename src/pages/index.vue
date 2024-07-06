<script setup lang="ts"></script>

<template>
  <div>
    <h1>Home Page</h1>
    <RouterLink :to="{ name: '/projects/' }">Go to Projects</RouterLink>
    <!-- <RouterLink :to="{ name: '/projects/[id]', params: { id: 1 } }">Go to Project 1</RouterLink> -->
    <!-- <RouterLink to="{ name: '/projects/[id]', params: { id: 1 } }">Go to Projects</RouterLink> -->
  </div>
</template>
