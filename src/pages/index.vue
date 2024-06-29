<script setup lang="ts">
import { supabase } from '@/lib/supabaseClient';
import { ref, onMounted } from 'vue';

const projects = ref();

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
    <h1>Home Page</h1>
    <RouterLink :to="{ name: '/projects/[id]', params: { id: 1 } }">Go to Project 1</RouterLink>
    <br />
    <RouterLink :to="{ name: '/projects/' }">Go to Projects</RouterLink>
    <!-- <RouterLink to="{ name: '/projects/[id]', params: { id: 1 } }">Go to Projects</RouterLink> -->
    <h2>Overview of the newest projects</h2>
    <div>
      <div v-for="project in projects" :key="project.id">
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
  </div>
</template>
