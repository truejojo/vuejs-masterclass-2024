<script setup lang="ts">
import { useRoute } from 'vue-router';

// import type { RouteNamedMap } from 'vue-router/auto-routes';
// import type { RouteLocationNormalizedLoaded } from 'vue-router';

// type ProjectRoute = RouteNamedMap['/projects/[id]']['params'];

// const route = useRoute() as RouteLocationNormalizedLoaded & { params: ProjectRoute };
// console.log(route);

const route = useRoute();
console.log(route);
</script>

<template>
  <div>
    <h1>Project {{ route.params?.id }}</h1>
    <h1>Project</h1>
    <RouterLink :to="{ name: '/' }">Go to Home</RouterLink>
  </div>
</template>
