<script setup lang="ts">
import { useRoute } from 'vue-router';

import type { RouteNamedMap } from 'vue-router/auto-routes';
import type { RouteLocationNormalizedLoaded } from 'vue-router';
import { supabase } from '@/lib/supabaseClient';
import { onMounted, ref } from 'vue';

type ProjectRoute = RouteNamedMap['/projects/[id]']['params'];

const project = ref();

const route = useRoute() as RouteLocationNormalizedLoaded & { params: ProjectRoute };

const getProject = async () => {
  const id = route.params.id;
  const { data, error } = await supabase.from('projects').select('*').eq('id', '1');

  if (error) console.log(error);
  return data;
};
console.log(route);

// const route = useRoute();
// console.log(route);
onMounted(async () => {
  project.value = await getProject();
});
</script>

<template>
  <div>
    <h1 v-if="project">{{ project.name }}</h1>
    <p>Project {{ route.params?.id }}</p>
  </div>
</template>
