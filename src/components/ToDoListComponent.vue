
<!-- List Component -->

<!-- Make the card for the list to exist on. -->
<template>
  <div>

    <!-- Dialog Prompts-->

    <q-dialog v-model="textprompt" persistent>
      <q-card style="min-width: 350px">
        <q-card-section>
          <div class="text-h6">New Task</div>
        </q-card-section>

        <!-- Text Prompt -->
        <q-card-section class="q-pt-none">
          <q-input dense v-model="task" autofocus @keyup.enter="textprompt = false; addTask(); data = '';" />
        </q-card-section>

        <q-card-actions align="right" class="text-primary">
          <q-btn flat label="Cancel" v-close-popup />
          <q-btn flat label="Add Task" v-close-popup @click="textprompt = false; addTask(); data = '';"/>
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="colorprompt" persistent>
      <q-card style="min-width: 350px">
        <q-card-section>
          <div class="text-h6">New Color</div>
        </q-card-section>

        <q-card-section>
          <q-color v-model="hex" no-header class="my-picker" />
        </q-card-section>

        <q-card-actions align="right" class="text-primary">
          <q-btn flat label="Cancel" v-close-popup />
          <q-btn flat label="Confirm" v-close-popup @click="colorprompt = false; addTask(); data = '';"/>
      </q-card-actions>
      </q-card>
    </q-dialog>

    <!-- List Card -->
    <q-card flat :style="{background: hex}">

      <!--List Title-->
      <q-card-section>
        <div class="row items-center">
          <div class="col">
            <QItemLabel class="text-weight-medium" @click.stop> {{title}}
              <q-popup-edit
                v-model="title"
                auto-save
                cover
                v-slot="scope"
                :validate="emptyStringValidation"
                :disable="!edit">
                  <q-input
                    v-model="scope.value"
                    dense
                    clearable
                    autofocus
                    @keyup.enter="scope.set"/>
              </q-popup-edit>
            </QItemLabel>
          </div>


          <!--Options Button-->
          <div class="col-auto">
            <q-btn color="white" round flat dense icon="more_vert">
              <q-menu cover auto-close :style="{background: hex}">
                <q-list>
                  <q-item clickable
                          @click="removeList()">
                    <q-item-section>Remove List</q-item-section>
                  </q-item>
                  <q-item clickable
                          @click="edit = true">
                    <q-item-section>Edit List</q-item-section>
                  </q-item>
                  <q-item clickable
                          @click="colorprompt = true">
                    <q-item-section>Change Color</q-item-section>
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
                <q-item-label
                  @click.stop> {{ taskItem.label }}
                  <q-popup-edit
                    v-model="taskItem.label"
                    auto-save
                    cover
                    v-slot="scope"
                    :validate="emptyStringValidation"
                    :disable="!edit">
                    <q-input
                      v-model="scope.value"
                      dense
                      clearable
                      autofocus
                      @keyup.enter="scope.set"/>
                  </q-popup-edit>
                </q-item-label>
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
                 @click="textprompt = true" />
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

        //Color
        hex: ref('#1d43ab'),

        //Dialog
        textprompt: ref(false),
        colorprompt: ref(false),
        task: ref(''),

        //List
        title: ref("New List"),
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
      },

      removeList() {
        this.$emit("Delete");
      },

      emptyStringValidation (val) {
        if (val) {
          return true
        }
        else {
          return false
        }
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
