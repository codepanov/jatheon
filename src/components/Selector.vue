<template>
  <div class="s-wrapper">
    <div class="s-selected" :class="{'s-expanded_border': expanded}" @click="expand()" ref="selected">
      {{ showSelected }}
      <img src="@/assets/icn-arrow-down.svg" alt="Arrow" ref="image">
    </div>
    <div class="s-modal" :class="{'s-modal-expanded': expanded}">
      <div class="s-search" v-show="payload.type == 'users'">
        <input type="text" placeholder="Search for a user..." v-model="search">
        <img 
          src="@/assets/search.svg" 
          alt="Search"
          class="icon-search"
        >
        <img 
          src="@/assets/icn-close.svg" 
          alt="Close"
          @click="reset_search" 
          v-show="search != ''" 
          class="icon-close"
        >
      </div>
      <div class="s-list" ref="modal">
        <div v-show="search == ''">
          <input id="sAll" type="checkbox" @click="selectAll" v-model="allSelected">
          <label for="sAll">Select all</label>
        </div>
        <ul>
          <li v-for="(item, i) in searchedItems" :key="i">
            <input type="checkbox" :id="item" :value="item" v-model="selectedItems" class="filled-in">
            <label :for="item">{{ item }}</label>
          </li>
        </ul>
        <span v-show="!searchedItems.length">No Results Found</span>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  props: {
    payload: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      showSelected: this.payload.message, // No user selected
      expanded: false,
      selectedItems: [],
      allSelected: false,
      search: ''
    }
  },
  methods: {
    expand() {
      let refs = [this.$refs.selected, this.$refs.modal]
      refs.map(ref => ref.addEventListener('mousedown', function(e){ e.preventDefault() }, false))
      
      if(!this.expanded)
        this.$refs.image.setAttribute('style', `transform: rotateZ(180deg)`)
      else
        this.$refs.image.setAttribute('style', `transform: rotateZ(0deg)`)
      this.expanded = !this.expanded
    },
    selectAll() {
      this.selectedItems = []
      this.allSelected = !this.allSelected
      if(this.allSelected)
        this.selectedItems = this.payload.list.map(item => item)
    },
    reset_search() {
      this.search = ''
    }
  },
  watch: {
    selectedItems() {
      let count = this.selectedItems.length
      if(!count)
        this.$emit('disable', true)
      else
        this.$emit('disable', false)
      count > 1 && !this.allSelected ?
        this.showSelected = `${count} selected` : this.allSelected == true ? this.showSelected = 'All selected' :
        this.showSelected = this.selectedItems[0]
      if(count == 0) {
        this.showSelected = this.payload.message // No user selected
      }
      this.allSelected = false
      console.log(this.selectedItems)
    },
    search() {
      console.log(this.searchedItems)
    }
  },
  computed: {
    searchedItems() {
      return this.payload.list.filter(item => {
        return item
        .toLowerCase()
        .includes(this.search.toLowerCase())
      })
    }
  }
}
</script>

<style>
.s-wrapper {
  position: relative;
}
.s-selected {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px 10px;
  width: 255px;
  background: white;
  position: relative;
  z-index: 2;
  cursor: pointer;
  background-color: #FFFFFF;
  border: 1px solid #9B9B9B;
  border-radius: 4px;
  font-size: 14px;
  margin-left: 15px;
}
.s-selected img {
  transition: transform 0.25s ease-in-out;
}
.s-modal {
  border: 1px solid blue;
  border-radius: 3px;
  padding: 10px;
  margin-top: 5px;
  margin-left: 15px;
  opacity: 0;
  position: absolute;
  top: -5px;
  transition: all 0.5s;
  z-index: -1;
  background: white;
  /* min-width: 255px; */
  background-color: #FFF;
  border: 1px solid #CFCFCF;
  border-radius: 4px;
  box-shadow: 0 3px 4px 0 rgba(0, 0, 0, 0.3);
  font-size: 14px;
}
.s-modal-expanded {
  opacity: 1;
  top: 50px;
  z-index: 0;
}
.s-expanded_border {
  border: 1px solid #00A88D;
}
.s-modal ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
.s-search {
  position:relative;
  display: flex;
  align-items: center;
}
.s-search input{
  padding: 10px;
  padding-left: 35px;
  width: 100%;
  background-color: #F4F4F4;
  border-radius: 4px;
  border: none;
}
.s-search input:focus {
  /* outline-color: #00A88D; */
  outline: none;
}
.icon-search {
  position: absolute;
  left: 10px;
}
.icon-close {
  position: absolute;
  right: 10px;
  cursor: pointer;
}
.s-list {
  margin-top: 12px;
  min-width: 255px;
  height: 300px;
  overflow-y: scroll;
  /* FireFox scrollbar */
  scrollbar-color: #CFCFCF #F4F4F4;
  scrollbar-width: thin;
}
/* Chrome scrollbar */
::-webkit-scrollbar {
  width: 7px;
}
::-webkit-scrollbar-track {
  background: #F4F4F4; 
}
::-webkit-scrollbar-thumb {
  background: #CFCFCF;
  border-radius: 7px;
}
::-webkit-scrollbar-thumb:hover {
  background: #b5b5b5; 
}
.s-list label {
  cursor: pointer;
}
.s-list label:hover {
  color: #00A88D;
}

/* CHECKBOX */

</style>