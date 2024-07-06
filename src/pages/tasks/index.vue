<script setup lang="ts">
import { supabase } from '@/lib/supabaseClient';
import { ref, onMounted } from 'vue';
import type { Tables } from '../../../database/types';

const tasks = ref<Tables<'tasks'>[] | null>(null);

const getTasks = async () => {
  const { data, error } = await supabase.from('tasks').select();

  if (error) console.log(error);
  return data;
};

onMounted(async () => {
  tasks.value = await getTasks();
});
</script>

<template>
  <div>
    <h1>Tasks Page</h1>
    <RouterLink to="/">Go Home</RouterLink>
    <h2>Overview of the newest Tasks</h2>
    <ul>
      <li v-if="tasks" v-for="task in tasks" :key="task.id">
        <h3>{{ task.name }}</h3>
        <p>{{ task.description }}</p>
        <div>
          <strong>{{ task.status }}</strong> - <small>{{ task.due_date }}</small>
        </div>
        <p>
          Go to the Project:
          <RouterLink :to="{ name: '/projects/[id]', params: { id: task.id } }">
            Go to Project {{ task.id }}
          </RouterLink>
        </p>
        <div>
          <p v-for="collaborator in task.collaborators" :key="collaborator">{{ collaborator }}</p>
        </div>
        <hr />
      </li>
    </ul>
  </div>
</template>
