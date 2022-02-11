<template>
  <div>
    <!-- New List button -->
    <div class="q-pa-md">
      <q-btn color="secondary"
        icon="add"
        clickable
        @click="addNewList()"
        label="Add new List" />
    </div>
    <!-- Start of List Components in Main Menu -->

    <q-page class="flex">

      <div class="column container">


        <div v-for="list in lists" :key ="list.title" class="cell" tabindex="0">
          <to-do-list-component style="max-width: 100%; width: 300px" />
        </div>


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
      lists: []
    }
  },

  methods:{
    addNewList(){
      this.lists.push(0);

    },

    deleteList(index){
      this.lists.splice(index, 1);
    }

  }
})
</script>
<style lang="sass" scoped>

.flex-break
  flex: 1 0 100% !important
  width: 0 !important

$x: 4

@for $i from 1 through ($x - 1)
  .container > div:nth-child(#{$x}n + #{$i})
    order: #{$i}

.container > div:nth-child(#{$x}n)
  order: #{$x}

.container
 height: 700px

 .cell
  width: 100%
  padding: 1px

  > div
    padding: 2px 2px

</style>


