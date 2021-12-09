
<!-- Containers for the List Items -->
<template>
  <div>
    <QItemLabel> List Title Here </QItemLabel>
    <QList ref="list">

      <to-do-item-component label= "This is the first Item"></to-do-item-component>
      <to-do-item-component label= "This is the second"></to-do-item-component>

    </QList>
    <q-btn
      round
      dense
      color="secondary"
      icon="add"
      @click="onClick"/>

  </div>
</template>

<script>
import Vue from 'vue'
import ToDoItemComponent from './ToDoItemComponent.vue';


  export default {

    name: 'ToDoList',
    components: { ToDoItemComponent },
    methods: {
      onClick(){
        var ComponentClass = Vue.extend(ToDoItemComponent);
        var instance = new ComponentClass({
          propsData: { label: 'I was added by clicking the button below' }
        })

        instance.$mount()
        this.$refs.list.appendChild(instance.$el);
      }
    }

  };
</script>
