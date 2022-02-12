<template>
  <q-page>

    <!-- Start of List Components in Main Menu -->

    <div class="flex q-pa-md">

      <div class="column container">


        <div v-for="(list, index) in lists" :key ="list.title" class="cell" tabindex="0">
          <to-do-list-component
            style="max-width: 100%; width: 275px"
            v-on:delete="deleteList(index)"/>
        </div>


      </div>

    </div>

    <!-- New List button -->
    <q-page-sticky position= "bottom-left" class="q-pa-sm">
      <q-btn color="secondary"
        icon="add"
        clickable
        @click="addNewList()"
        label="Add new List" />
    </q-page-sticky>

  </q-page>
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


