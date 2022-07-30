<template>
  <div
    class="alert text-white font-weight-bold"
    role="alert"
    :class="getClasses(color, dismissible)" style="position: fixed;width: 100%;opacity: 0.8" v-show="show_msg">
    <span class="alert-icon">
      <i :class="getIcon(icon)" />
    </span>
    <span class="alert-text">
      {{ message }}
    </span>
    <button
      v-if="dismissible"
      type="button"
      class="btn-close d-flex justify-content-center align-items-center"
      data-bs-dismiss="alert"
      aria-label="Close"
    >
      <span aria-hidden="true" class="text-lg font-weight-bold">&times;</span>
    </button>
  </div>
</template>

<script>
export default {
  data(){
    return{
      show_msg:true
    }
  },
  name: "note-alert",
  props: {
    color: {
      type: String,
      default: "success",
    },
    icon: String,
    dismissible: {
      type: Boolean,
      default: false,
    },
    message:{
      type: String,
      default: ""
    }
  },
  methods: {
    getClasses: (color, dismissible) => {
      let colorValue, dismissibleValue;

      colorValue = color ? `alert-${color}` : null;

      dismissibleValue = dismissible ? "alert-dismissible fade show" : null;

      return `${colorValue} ${dismissibleValue}`;
    },
    getIcon: (icon) => (icon ? icon : null),
  },
  mounted() {
    setTimeout(()=>{
      this.show_msg=false;
    },10000)
  }
};
</script>
<style>
/*.alert{*/
/*  position: fixed;*/
/*  opacity: 0.9;*/
/*  width: 100%;*/
/*}*/
</style>

<!--<style>-->
<!--.fadenum{-->
<!--  animation:fade 2s 1;-->
<!--}-->
<!--@keyframes fade{-->
<!--  0%{opacity: 0;}-->
<!--  100%{opacity: 0.9;}-->
<!--}-->
<!--</style>-->