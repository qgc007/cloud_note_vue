<template>
  <i class="ni ni-basket">1111</i>
  <Note-alert color="success" icon="ni ni-check-bold" dismissible>
    <strong>Dark!</strong> This is a dismissible alert!
  </Note-alert>
</template>

<script>
import NoteAlert from "@/components/NoteAlert.vue";
export default {
  components: {
    NoteAlert
  },
}
</script>