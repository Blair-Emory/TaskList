<template>
  <q-page class="flex flex-center">
    <div>
      <to-do-list-component style= "max-width: 100%; width: 350px"/>
    </div>
  </q-page>
</template>

<script>
import { defineComponent } from 'vue';
import ToDoListComponent from '../components/ToDoListComponent.vue'

export default defineComponent({
  name: 'PageIndex',

  components: {
    ToDoListComponent
  }
})
</script>
