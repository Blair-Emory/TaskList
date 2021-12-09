<!-- Individual items found inside todo lists -->
<template>
  <div>
    <QItem class="q-pa-sm">
      <q-checkbox v-model="val"/>
      <QItemLabel> {{label}} </QItemLabel>
    </QItem>
  </div>
</template>

<script>
import { ref } from 'vue';
  export default {

    props: {
      label: { required: true, type: String }
    },

    setup() {
      return {
        val: ref(true)
      }
    }
  }
</script>
