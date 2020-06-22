<template>
  <div class="s-wrapper">
    <div class="s-selected" :class="{'s-expanded_border': expanded}" @click="expand()" ref="selected">
      {{ showSelected }}
      <img src="@/assets/icn-arrow-down.svg" alt="Arrow" ref="image">
    </div>
    <!-- animates modal element by binding ...expended class -->
    <div class="s-modal" :class="{'s-modal-expanded': expanded}"> 
      <div class="s-search" v-show="payload.type == 'users'">
        <input type="text" placeholder="Search for a user..." v-model="search">
        <img 
          src="@/assets/search.svg" 
          alt="Search"
          class="icon-search"
        >
        <!-- imag shows if search property is not empty string -->
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
    /**
     * preventing text and img selection on doubleclick
     * putting refs in array and mapping to avoid redundacy
     */
    expand() {
      let refs = [this.$refs.selected, this.$refs.modal]
      refs.map(ref => ref.addEventListener('mousedown', function(e){ e.preventDefault() }, false))
      
      // rotating arrow on click
      if(!this.expanded)
        this.$refs.image.setAttribute('style', `transform: rotateZ(180deg)`)
      else
        this.$refs.image.setAttribute('style', `transform: rotateZ(0deg)`)
      this.expanded = !this.expanded
    },
    selectAll() {
      this.selectedItems = []
      this.allSelected = !this.allSelected
      if(this.allSelected) //has to check if true because line above will switch to false at one point and we do not want to map users in that case, we just need an empty array of selected users
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
      // logic that handles selected users message
      count > 1 ?
        this.showSelected = `${count} selected` :
        this.showSelected = this.selectedItems[0]
      if(count == 0) {
        this.showSelected = this.payload.message // No user selected
      }
      // whenever something changes in selectedUsers array we reset this field to its default state (false). It has to be false because SELECT ALL is connected through v-model
      this.allSelected = false
      console.log(this.selectedItems)
    },
    search() {
      console.log(this.searchedItems)
    }
  },
  computed: {
    /**
     * this computes through v-modeled search input
     * by filtering every character
     * and compares through includes
     * with every iteration of the current array of users
     */
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
  font: inherit;
  height: 15px;
}
.s-search input:focus {
  outline-color: #00A88D;
  /* outline: none; */
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
@media screen and (max-width: 1170px) {
  .s-modal-expanded {
    z-index: 1;
  }
  .s-selected {
    width: 180px;
  }
}

/* CHECKBOX */
/* .s-list input[type="checkbox"] {
  display: contents;
}
.s-list input[type="checkbox"].filled-in:checked+label:after {
    top: 0px;
    width: 19px;
    height: 19px;
    border: 2px solid #26a69a;
    background-color: #26a69a;
    z-index: 0;
    border-radius: 4px;
}
.s-list input[type="checkbox"].filled-in+label:before, [type="checkbox"].filled-in+label:after {
    content: '';
    left: 0;
    position: absolute;
    transition: border .25s,background-color .25s,width .2s .1s,height .2s .1s,top .2s .1s,left .2s .1s;
    z-index: 1;
}
.s-list input[type="checkbox"].filled-in+label:after {
    border-radius: 2px;
}
.s-list input[type="checkbox"].filled-in:checked+label:before {
    top: 0;
    left: 1px;
    width: 8px;
    height: 13px;
    border-top: 2px solid transparent;
    border-left: 2px solid transparent;
    border-right: 2px solid #fff;
    border-bottom: 2px solid #fff;
    -webkit-transform: rotateZ(37deg);
    transform: rotateZ(37deg);
    -webkit-transform-origin: 100% 100%;
    transform-origin: 100% 100%;
}
.s-list input[type="checkbox"].filled-in+label:before, [type="checkbox"].filled-in+label:after {
    content: '';
    left: 0;
    position: absolute;
    transition: border .25s,background-color .25s,width .2s .1s,height .2s .1s,top .2s .1s,left .2s .1s;
    z-index: 1;
}
.s-list input[type="checkbox"]:checked+label:before {
    top: -4px;
    left: -3px;
    width: 12px;
    height: 22px;
    border-top: 2px solid transparent;
    border-left: 2px solid transparent;
    border-right: 2px solid #26a69a;
    border-bottom: 2px solid #26a69a;
    -webkit-transform: rotate(40deg);
    -moz-transform: rotate(40deg);
    -ms-transform: rotate(40deg);
    -o-transform: rotate(40deg);
    transform: rotate(40deg);
    -webkit-backface-visibility: hidden;
    -webkit-transform-origin: 100% 100%;
    -moz-transform-origin: 100% 100%;
    -ms-transform-origin: 100% 100%;
    -o-transform-origin: 100% 100%;
    transform-origin: 100% 100%;
}
.s-list input[type="checkbox"]+label:before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 18px;
    height: 18px;
    z-index: 0;
    border: 2px solid #5a5a5a;
    border-radius: 1px;
    margin-top: 2px;
    -webkit-transition: 0.2s;
    -moz-transition: 0.2s;
    -o-transition: 0.2s;
    -ms-transition: 0.2s;
    transition: 0.2s;
}
.s-list input[type="checkbox"]+label {
    position: relative;
    padding-left: 28px;
    cursor: pointer;
    display: inline-block;
    height: 25px;
    line-height: 25px;
    font-size: 1rem;
    -webkit-user-select: none;
    -moz-user-select: none;
    -khtml-user-select: none;
    -ms-user-select: none;
}
.s-list label {
    font-size: 0.8rem;
    color: #9e9e9e;
}
*, *:before, *:after {
    box-sizing: inherit;
} */
</style>