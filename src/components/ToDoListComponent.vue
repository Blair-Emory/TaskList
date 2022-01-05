
<!-- Containers for the List Items -->

<!-- Make the card for the list to exist on. -->
<template>
  <q-card flat>

    <!--List Title-->
    <q-card-section >
      <div class="row items-center">
        <div class="col">
          <QItemLabel class="text-weight-medium"> {{title}} </QItemLabel>
        </div>


        <!--Options Button-->
        <div class="col-auto">
         <q-btn color="white" round flat dense icon="more_vert">
           <q-menu cover auto-close>
             <q-list>
               <q-item clickable>
                  <q-item-section>Remove List</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Edit List</q-item-section>
                </q-item>
                <q-item clickable>
                  <q-item-section>Share</q-item-section>
                </q-item>
              </q-list>
            </q-menu>
          </q-btn>
        </div>
      </div>
    </q-card-section>

    <q-separator/>

    <!-- To-Do items -->
    <q-card-section>
      <div>

        <!-- This will iterate through every task in tasks list and create an item for it -->
        <q-item
          v-for="(taskItem, index) in tasks"
          :key="taskItem.label"
          @click="taskItem.done = !taskItem.done"
          :class="{ 'done' : taskItem.done }"
          class="row items-center justify-between"
          clickable
          v-ripple>

          <!-- Task Item -->
            <div class="col-auto">
              <q-item-section avatar>
                <q-checkbox v-model="taskItem.done"
                            color="accent"
                            class="no-pointer-events" />
              </q-item-section>
            </div>
            <div class="col">
              <q-item-section>
                <q-item-label> {{ taskItem.label }} </q-item-label>
              </q-item-section>
            </div>
            <div class="col-auto">
              <q-item-section>
                <q-btn round
                       flat
                       dense
                       icon="delete"
                       @click.stop="deleteTask(index)"/>
              </q-item-section>
            </div>


        </q-item>
      </div>
    </q-card-section>

    <!-- Add new Item button -->
    <q-card-section>
      <div class="col-auto">
        <q-btn
          round
          dense
          color="secondary"
          icon="add"
          clickable
          @click="newTask"/>
      </div>
    </q-card-section>

  </q-card>
</template>

<script>
import ToDoItemComponent from './ToDoItemComponent.vue';
import { useQuasar } from 'quasar';

  export default {

    name: 'ToDoList',

    data(){
      return {
        title: 'New List',
        tasks: [
          {
            label: 'Blah',
            done: false
          },
          {
            label: "Blah Blah",
            done: false
          },
          {
            label: "some really long string to see if this wraps or extends the card",
            done: true
          },
          {
            label: "Even longer label to see if this truely messes up everything that goes on within this card. Lets see how this goes. Woop Woop.",
            done: true
          }
        ]
      }
    },
    setup() {
      const $q = useQuasar()

      function newTask () {

        $q.dialog({
          dark: true,
          title: 'New Task',
          prompt: {
            model: '',
            type: 'text'
          },
          cancel: true,
          persistent: true
        }).onOk(data => {

          //Create the new tasks
          this.tasks.insert({
            label: data,
            done: false
          })

        }).onCancel(() => {
          //Cancel creating new task
        }).onDismiss(() => {
          //Triggered on both Okay and Cancelled
        })
      }

      return { newTask }
    },
    methods: {
      addTask(data){


      },

      deleteTask(index) {
        this.tasks.splice(index, 1);
      }


    },


  };
</script>

<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: rgba(187, 187, 187, 0.5);
    }
  }
</style>
