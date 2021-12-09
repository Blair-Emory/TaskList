
<!-- Containers for the List Items -->

<!-- Make the card for the list to exist on. -->
<template>
  <q-card flat bordered="my-card">

    <!--List Title-->
    <q-card-section >
      <div class="row items-center">
        <div class="col">
          <QItemLabel class="text-weight-medium"> {{title}} </QItemLabel>
        </div>


        <!--Options Button-->
        <div class="col-auto">
         <q-btn color="grey-7" round flat dense icon="more_vert">
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
      <div class="items-left">
        <QList ref="list">

          <to-do-item-component label= "This is the first Item"></to-do-item-component>
          <to-do-item-component label= "This is the second"></to-do-item-component>

        </QList>
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
          @click="onClick"/>
      </div>
    </q-card-section>

  </q-card>
</template>

<script>
import ToDoItemComponent from './ToDoItemComponent.vue';


  export default {

    name: 'ToDoList',
    components: { ToDoItemComponent },
    props: {
      title: {required: false, type: String, default: 'New List'}
    },
    methods: {
      onClick(){

      }
    }

  };
</script>
