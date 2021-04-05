<template lang="pug">
div
  p HelloWorld
  label Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
  table.grid(v-if="response && response.length")
    thead.grid-header
        th(v-for="col in cols" v-html="col.title")
    tbody
      tr(v-for="item in response")
        td(v-for="col in cols")
          span {{item[col.key]}}
          span(v-if="col.key == 'command'") 
            a.button(href="#")
              span.icon.edit
              span Edit
            a.button(href="#")
              span.icon.delete
              span Delete
</template>
<script>
export default {
  props: ['cols', 'response']
}
</script>
<style scoped>
table {
  width: 100%
}
.grid-header {
    border-bottom-width: 1px;
    border-color: #dee2e6;
    color: #212529;
    background-color: #f8f9fa;
}
.grid th {
  padding: .75rem .75rem;
  white-space: nowrap;
}
.grid td {
  padding: .75rem .75rem;
  white-space: nowrap;
}
.button {
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
tr:nth-child(2n) {
  background-color: rgba(0,0,0,.05);
}
</style>