<script setup lang="ts">
import { supabase } from '@/lib/supabaseClient';
import { ref, onMounted } from 'vue';
import type { Tables } from '../../../database/types';

const projects = ref<Tables<'projects'>[] | null>(null);

const getProjects = async () => {
  const { data, error } = await supabase.from('projects').select();

  if (error) console.log(error);
  return data;
};

onMounted(async () => {
  projects.value = await getProjects();
});
</script>

<template>
  <div>
    <h1>Projects Page</h1>
    <RouterLink to="/">Go Home</RouterLink>
    <h2>Overview of the newest projects</h2>
    <div v-if="projects" v-for="project in projects" :key="project.id">
      <h2>{{ project.name }}</h2>
      <p>Project Status: {{ project.status }}</p>
      <h3>Number of the Teams</h3>
      <ul>
        <li v-for="collaborator in project.collaborators" :key="collaborator">
          {{ collaborator }}
        </li>
      </ul>
      <hr />
    </div>
  </div>
</template>
