<template lang="pug">
.input_conteiner
  input(type='text' v-model='value' @input='returnInput')
  span {{measure}}
  button.delete(@click="clear" :tabindex="-1") ✖
</template>

<script>
export default {
  props: ['defaultValue', 'measure'],
  data () {
    return {      
      value: this.defaultValue
    }
  },
  methods: {
    returnValue() {
      if (this.value === '') {
        this.value = null
      }
      if (this.value != null) {
        this.value = this.value.replace(/[,]/g, '.')
      }
      this.$emit('input', this.value)
    }
  },
    clear () {
      this.value = null
      this.$emit('input', this.value)
    },
}
</script>

<style scoped>
.input_container {
  display: grid;
  grid-template-columns: 65% auto 10%;
  grid-template-rows: 2fr;
  margin: 22px 20px 0 20px;
  }
input {
  border-radius: 4px 0px 0px 4px;
  height: 30px;
  border: 1px solid #ccc;
  font-size: 16px;
  color: #212121;
  padding-left: 7px;
  transition: border-color ease-in-out .15s,box-shadow ease-in-out .15s;
  outline: none;
  }
span {
  border: 1px solid #ccc;
  border-left: none;
  display: grid;
  font-size: 13px;
  align-content: center;
  justify-content: center;
  }
input:focus {
  border-radius: 4px 4px 4px 4px;
  border-color: rgba(26, 163, 255, 0.8);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.075) inset, 0 0 8px rgba(0, 153, 255, 0.6);
  }
button {
  border-radius: 0px 4px 4px 0px;
  border: 1px solid #ccc;
  border-left: none;
  background: white;
  display: grid;
  align-content: center;
  justify-content: center;
  cursor: pointer;
  outline: none;
  }
.delete:hover {
  transition: all, .3s;
  color: #e2211d;
  font-weight: bold;
  }
</style>