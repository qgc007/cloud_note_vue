<template>
  <div class="form-check">
    <input class="form-check-input" type="checkbox" :name="name" :id="id" :checked="checked" @change="onchange"/>
    <label :for="id" class="custom-control-label">
      <slot />
    </label>
  </div>
</template>

<script>
export default {
  name: "note-checkbox",
  props: {
    name: String,
    id: String,
    checked: String,
  },
  methods:{
    onchange(e){
      this.$emit('update:checked', e.target.checked);
    }
  }
};
</script>
