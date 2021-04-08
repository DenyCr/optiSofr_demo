<template lang="pug">
.v-popup
  .v-popup__header
    span Edit
    span 
      i.material-icons(@click="closePopup") close
  .v-popup__content
    slot
  .v-popup__footer
    button.close_modal(@click="closePopup") Cansel
    button.submit_modal Update

</template>

<script>
export default {
  name: "v-popup",
  props: {},
  data() {
    return {}
  },
  methods: {
    closePopup() {
      this.$emit('closePopup')
    }
  }
}
</script>
<style scoped>
.v-popup {
  padding: 16px;
  width: 400px;
  background: #FFF;
  box-shadow: 0 0 17px 0 #e7e7e7;
  z-index: 10;
  border-radius: 10pt;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
  .v-popup__header, .v-popup__footer {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }
  
  .v-popup__content {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 10px;
  }
  
  .submit_modal {
    padding: 8px;
    color: #FFF;
    background: #26ae68;
  }
  
  .close_modal {
    padding: 8px;
    color: #FFF;
    background: red;
  }
</style>
