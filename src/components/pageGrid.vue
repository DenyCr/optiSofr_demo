<template lang="pug">
div
  table.grid(v-if="response && response.length && page")
    thead.grid-header
      
      tr
        th(colspan=6)
          button.button
            span.icon.add.fa-plus
            i.fal.fa-plus
            span Add new record
      th(v-for="col in cols" v-html="col.title")
    tfoot
      tr
        td(colspan=3)
          nav
            .pagination_grid
              // «
              button.button(@click="goToFirstPage" v-if="reversedPage>1 && maxPages>buffer+1") &laquo;
              // ‹
              button.button(@click="prevPage" v-if="reversedPage>1") &lsaquo;
              button.button(v-for="page in maxSize" @click="goToPage(page)" :class="reversedPage == page ? 'activatePages' : ''" v-bind:disabled="reversedPage == page ? true : false") {{ page }}
              // ›
              button.button(@click="nextPage" v-if="reversedPage<maxPages") &rsaquo;
              // »
              button.button(@click="goToLastPage" v-if="reversedPage<maxPages && maxPages>buffer+1") &raquo;

        td.recordSteer(colspan=3)        
          span {{page*20-19}} - {{(page*20 < count) ? page*20 : count}} of {{count}} items
    tbody
      tr(v-for="item in data")
        td(v-for="col in cols")
          span(v-if="col.key === 'UnitPrice'") $ {{item[col.key].toFixed(2)}} 
          span(v-if="col.key !== 'UnitPrice'") {{item[col.key]}}
          
          span(v-if="col.key === 'command'") 
            a.button(href="#")
              span.icon.edit
              span Edit
            a.button(href="#")
              span.icon.delete
              span Delete
    
  span.error(v-if="!page") Данные были не получены или ошибочны, перезагрузите страницу
</template>
<script>
export default {
  props: ['cols', 'response'],
  data () {
    return {
      limit: 20,
      maxPages: 5,
      maxSize: [],
      data: [],
      count: 0,
      page: 1,
      buffer: 2,
      offset: 0
    }
  },
  created () {
    this.page = 1
    let par1 = 1
    let par2 = 2 + this.buffer * 2
    
    this.count = this.response.length

    this.maxPages = Math.ceil(this.count / this.limit)
    this.maxSize = []
    for (
      let index = this.maxPages > 6 ? par1 : 1;
      index < (this.maxPages > 6 ? par2 : this.maxPages + 1);
      index++
    ) {
      this.maxSize.push(index)
    }
    
    let min = this.page * this.limit - this.limit
    let max = (this.page * this.limit < this.count) ? this.page * this.limit : this.count
    for ( let index = min; index < max; index++ ) {
      this.data.push(this.response[index])
    }
    this.offset = min + 1
  },
  methods: {
    getDataPage () {
      this.page = this.offset !== 0 ? this.offset / this.limit + 1 : 1
      let par1 = 0
      let par2 = 0
      if ( this.page > this.buffer && this.page < this.maxPages - this.buffer + 1 ) {
        par1 = this.page - this.buffer
        par2 = this.page + this.buffer + 1
      } else {
        if (this.page <= this.buffer) {
          par1 = 1
          par2 = 2 + this.buffer * 2
        }
        if (this.page >= this.maxPages - this.buffer + 1) {
          par1 = this.maxPages - 2 * this.buffer
          par2 = this.maxPages + 1
        }
      }
      console.log(par1,par2)
      let min = this.page * this.limit - this.limit
      let max = (this.page * this.limit < this.count) ? this.page * this.limit : this.count
      console.log(min,max)
      this.data = []
      for ( let index = min; index < max; index++ ) {
        this.data.push(this.response[index])
      }
    },  
    nextPage () {
      this.offset = this.offset + this.limit
      this.getDataPage()
      this.goTop()
    },
    prevPage () {
      this.offset = this.offset - this.limit
      this.getDataPage()
      this.goTop()
    },
    goToFirstPage () {
      this.offset = 0
      this.getDataPage()
      this.goTop()
    },
    goToLastPage () {
      this.offset = this.limit * (this.maxPages - 1)
      this.getDataPage()
      this.goTop()
    },
    goToPage (page) {
      this.offset = this.limit * (page - 1)
      this.getDataPage()
      this.goTop()
    },
    goTop () {
      document.location.href = '#'
    },
  },
  computed: {
    reversedPage: function () {
      return this.page
    },
  }
}

</script>
<style scoped>
table {
  width: 100%;
  border-color: #dee2e6;
  border-width: 1px;
  border-style: solid;
  box-sizing: border-box;
  text-align: left;
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
  border-color: rgba(33,37,41,.125);
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
.error {
  font-size: 35px;
  font-weight: 700;
  color: #FFF;

  display: inline-block;
  padding: 50px;
  border-radius: 20px;

  background-image: linear-gradient( 90deg , #CC2E5D, #FF5858);
  box-shadow: 10px 10px rgba(0,0,0,.05);
}
.activatePages {
  
  border-color: #a0eaec;
  background-image: linear-gradient( 90deg , #2eb4cc, #58ffb1);
  box-shadow: 3px 3px rgba(0,0,0,.12);
}
.recordSteer {
  background-image: linear-gradient( 90deg , #CC2E5D, #FF5858);
}
</style>