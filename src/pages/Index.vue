<template>

  <div>
    <!-- New List button -->
    <div class="q-pa-md">
      <q-btn color="secondary"
             icon="add"
             clickable
             @click="addNewList"
             label="Add new List" />
    </div>

    <!-- Start of List Components in Main Menu -->

    <q-page class="flex flex-center">
      <div class="q-pa-md">
        <to-do-list-component style="max-width: 100%; width: 350px" />
      </div>
    </q-page>

  </div>
</template>

<script>
import { defineComponent } from 'vue';
import ToDoListComponent from '../components/ToDoListComponent.vue'

export default defineComponent({
  name: 'PageIndex',

  components: {
    ToDoListComponent
  },
  data() {
    return {
      //List o Lists
      lists: [ ]
    }
  },

  methods:{
    addNewList(){


    },

    deleteList(index){
      this.lists.splice(index, 1);
    }

  }
})
</script>


