<template>
  <div class="s-wrapper">
    <div class="s-selected" @click="expand()" ref="selected">
      {{ showSelected }}
      <img src="@/assets/icn-arrow-down.svg" alt="Arrow" ref="image">
    </div>
    <div class="s-modal" :class="{'s-modal-expanded': expanded}" ref="modal">
      <div class="s-search">
        <input type="text" placeholder="Search for a user..." v-model="search">
        <img 
          src="@/assets/search.svg" 
          alt="Search" 
          ref="search" 
          class="icon-search"
        >
        <img 
          src="@/assets/icn-close.svg" 
          alt="Close" 
          ref="close" 
          @click="reset_search" 
          v-show="search != ''" 
          class="icon-close"
        >
      </div>
      <div class="s-list">
        <div v-show="search == ''">
          <input type="checkbox" @click="selectAll" v-model="allSelected">
          <label>Select all</label>
        </div>
        <ul>
          <li v-for="(user, i) in searchedUsers" :key="i">
            <input type="checkbox" :id="user" :value="user" v-model="selectedUsers">
            <label :for="user">{{ user }}</label>
          </li>
        </ul>
        <span v-show="!searchedUsers.length">No Results Found</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [
        'zena.huels@gmail.com',
        'welch.lauren@gmail.com',
        'tillman.marisa@cole.com',
        'mariela.lesch@gmail.com',
        'abshire.bertrand@hotmail.com',
        'bledner@hotmail.com',
        'skreiger@jacobs.biz',
        'dbrakus@yahoo.com',
        'tyra.heidenreich@powlowski.com',
        'vwehner@tremblay.com',
        'kessler.eugene@gmail.com',
        'murray.spencer@wisozk.info',
        'toby63@welch.com',
        'rashawn51@yahoo.com',
        'kelsi.crona@crona.net',
        'keebler.monty@mann.com',
        'blanda.rhett@gaylord.com',
        'lebsack.kristy@hotmail.com',
        'bridget33@schuster.com',
        'herzog.maymie@wehner.com'
      ],
      showSelected: 'No user selected',
      expanded: false,
      selectedUsers: [],
      allSelected: false,
      search: ''
    }
  },
  methods: {
    expand() {
      // preventing text and img selection
      let refs = [this.$refs.selected, this.$refs.modal] // putting refs in array and mapping to avoid redundacy
      refs.map(ref => ref.addEventListener('mousedown', function(e){ e.preventDefault(); }, false))
      
      if(!this.expanded)
        this.$refs.image.setAttribute('style', `transform: rotateZ(180deg)`)
      else
        this.$refs.image.setAttribute('style', `transform: rotateZ(0deg)`)
      this.expanded = !this.expanded
    },
    selectAll() {
      this.selectedUsers = []
      this.allSelected = !this.allSelected
      if(this.allSelected )
        this.users.map(user => this.selectedUsers.push(user))
    },
    reset_search() {
      this.search = ''
    }
  },
  watch: {
    selectedUsers() {
      let count = this.selectedUsers.length
      count > 1 ?
        this.showSelected = `${count} selected` :
        this.showSelected = this.selectedUsers[0]
      if(count == 0) {
        this.showSelected = 'No user selected'
      }
      this.allSelected = false
      console.log(this.selectedUsers)
    },
    search() {
      console.log(this.searchedUsers)
    }
  },
  computed: {
    searchedUsers() {
      return this.users.filter(user => {
        return user
        .toLowerCase()
        .includes(this.search.toLowerCase())
      })
    }
  }
}
</script>

<style>
.s-selected {
  display: flex;
  align-items: center;
  justify-content: space-between;
  border: 1px solid red;
  border-radius: 3px;
  padding: 10px;
  width: 265px;
  background: white;
  position: relative;
  z-index: 2;
  cursor: pointer;
}
.s-selected img {
  transition: transform 0.25s ease-in-out;
}
.s-modal {
  border: 1px solid blue;
  border-radius: 3px;
  padding: 10px;
  min-width: 265px;
  margin-top: 5px;
  opacity: 0;
  position: absolute;
  top: -5px;
  transition: all 0.5s;
  z-index: -1;
  background: white;
  width: fit-content;
  overflow-y: scroll;
}
.s-modal-expanded {
  opacity: 1;
  top: 45px;
  z-index: 0;
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
  border-radius: 5px;
  width: 100%;
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
  height: 300px;
}
.s-list label {
  cursor: pointer;
}
.s-list label:hover {
  color: red;
}
</style>