<!-- Individual items found inside todo lists -->
<template>
  <div>
    <QItem class="q-pr-sm">
      <q-checkbox v-model="val" color="accent"/>
      <QItemLabel> {{label}} </QItemLabel>
    </QItem>
  </div>
</template>

<script>
import { ref } from 'vue';
  export default {

    data() {
      return {
        label: 'New Task',
        done: false
      }
    },

    setup() {
      return {
        val: ref(true)
      }
    }
  }
</script>
