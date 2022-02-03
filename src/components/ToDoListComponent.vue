
<!-- List Component -->

<!-- Make the card for the list to exist on. -->
<template>
  <div>

    <!-- Dialog Prompts-->

    <q-dialog v-model="prompt" persistent>
      <q-card style="min-width: 350px">
        <q-card-section>
          <div class="text-h6">New Task</div>
        </q-card-section>

        <!-- Text Prompt -->
        <q-card-section class="q-pt-none">
          <q-input dense v-model="task" autofocus @keyup.enter="prompt = false; addTask(); data = '';" />
        </q-card-section>

        <q-card-actions align="right" class="text-primary">
          <q-btn flat label="Cancel" v-close-popup />
          <q-btn flat label="Add Task" v-close-popup @click="addTask(); data = '';"/>
        </q-card-actions>
      </q-card>
    </q-dialog>

    <!-- List Card -->
    <q-card flat>

      <!--List Title-->
      <q-card-section>
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
                  <q-item clickable
                          @click="edit = true">
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

      <q-separator />

      <!-- To-Do items -->
      <q-card-section>
        <div>

          <!-- This will iterate through every task in tasks list and create an item for it -->
          <q-item v-for="(taskItem, index) in tasks"
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
            <!-- edit task - only visible when list is in edit mode -->
            <div class="col-auto">
              <q-item-section v-show="edit">
                <q-btn round
                       flat
                       size="sm"
                       dense
                       icon="edit"
                       @click.stop="editTask(index)"/>
              </q-item-section>
            </div>
            <!-- delete task - only visible when list is in edit mode -->
            <div class="col-auto">
              <q-item-section v-show="edit">
                <q-btn round
                       flat
                       size="sm"
                       dense
                       icon="delete"
                       @click.stop="deleteTask(index)" />
              </q-item-section>
            </div>


          </q-item>
        </div>
      </q-card-section>

      <!-- Add new Item button, Confirm Edits button -->
      <q-card-section class="row items-center justify-between">

        <!-- Add Task -->
        <div class="col-auto">
          <q-btn round
                 dense
                 color="secondary"
                 icon="add"
                 clickable
                 @click="prompt = true" />
        </div>

        <!-- Confirm Changes (Only shows when list is in edit mode) -->
        <div class="col-auto" v-show="edit">
          <q-btn round
                 dense
                 color="secondary"
                 icon="check"
                 clickable
                 @click="edit=false" />
        </div>
      </q-card-section>

    </q-card>
  </div>
</template>

<script>
  import { ref } from 'vue';
  export default {

    name: 'ToDoList',

    data(){
      return {
        //Edit
        edit: ref(false),

        //Dialog
        prompt: ref(false),
        task: ref(''),

        //List
        title: ref('New List'),
        tasks: [
            {
              label: "example Task",
              done: false,
              edit: false
            }
         ]
      }
    },

    methods: {

      addTask(){

        var taskValue = this.task

        if (taskValue != '') {
          this.tasks.push({
            label: taskValue,
            done: false,
            edit: false
          })

          this.task = ''
        }

      },

      editTask(index) {
          //Some way to edit individual task items
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
