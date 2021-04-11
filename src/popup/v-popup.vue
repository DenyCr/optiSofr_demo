<template lang="pug">
.popup_wrapper(ref='popup_wrapper')
  .v-popup
    .v-popup__header
      span {{popupTitle}}
      span 
        i.material-icons(@click="closePopup") close
    .v-popup__content
      slot
    .v-popup__footer
      button.close_modal(@click="closePopup") Cancel
      button.submit_modal(@click="eventPopup") {{popupSubmitButton}}

</template>

<script>
export default {
  name: "v-popup",
  props: {
    popupTitle: {
      type: String,
      default: "Product"
    },
    popupSubmitButton: {
      type: String,
      default: "Update"
    }
  },
  data() {
    return {}
  },
  methods: {
    closePopup() {
      this.$emit('closePopup')
    },
    eventPopup () {      
      this.$emit('eventPopup')
    }
  },
  mounted() {
    let vm=this
    document.addEventListener('click', function(item) {
      if (item.target === vm.$refs['popup_wrapper']) {
        vm.closePopup()
      }
    })
  }
}
</script>
<style scoped>
.popup_wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  right: 0;
  left: 0;
  top: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.856);
  backdrop-filter: blur(8px);
  z-index: 2;
}
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
    font-size: 1.2rem;
    font-weight: bold;
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
  button {    
    margin-left: .16em;
    margin-right: .16em;
    text-decoration: none;
    border-color: #e4e7eb;
    color: #212529;
    background-color: #e4e7eb;
    border-radius: .25rem;
    padding: .375rem .75rem;
    box-sizing: border-box;
    border-width: 1px;
    border-style: solid;
    font-size: 1rem;
    line-height: 1.5;
    font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,"Noto Sans","Liberation Sans",sans-serif,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol","Noto Color Emoji";
    text-align: center;
    text-decoration: none;
    white-space: nowrap;
    display: -ms-inline-flexbox;
    display: inline-flex;
    -ms-flex-align: center;
    align-items: center;
    -ms-flex-pack: center;
    justify-content: center;
    vertical-align: middle;
    -webkit-user-select: none;
    -ms-user-select: none;
    user-select: none;
    cursor: pointer;
    outline: 0;
    -webkit-appearance: none;
    position: relative;
  }
</style>
