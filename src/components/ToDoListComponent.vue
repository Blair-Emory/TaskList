
<!-- Containers for the List Items -->
<template>
  <div>
    <QItemLabel> List Title Here </QItemLabel>
    <QList>

      <to-do-item-component label= "The label goes here Emory"></to-do-item-component>
      <to-do-item-component label= "This is a second item Bitch"></to-do-item-component>

    </QList>
  </div>
</template>

<script>
import ToDoItemComponent from './ToDoItemComponent.vue';


  export default {

    name: 'ToDoList',
    components: { ToDoItemComponent },

  };
</script>
