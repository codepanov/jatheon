<template>
  <div class="s-wrapper">
    <div class="s-selected" @click="expand()" ref="selected">
      {{ showSelected }}
      <img src="@/assets/icn-arrow-down.svg" alt="Arrow" ref="image">
    </div>
    <div class="s-modal" :class="{'s-modal-expanded': expanded}">
      <div class="s-search">
        <input type="text" placeholder="Search" v-model="search">
        <img src="@/assets/icn-close.svg" alt="Close" ref="close" @click="reset_search">
      </div>
      <div class="s-list">
        <input type="checkbox" @click="selectAll" v-model="allSelected">
        <label>Select all</label>
        <ul>
          <li v-for="(user, i) in searchedUsers" :key="i">
            <input type="checkbox" :value="user.name" v-model="selectedUsers">
            <label :for="user.name">{{ user.name }}</label>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [
        {name: 'Patrick'},
        {name: 'Evan'},
        {name: 'Christian'},
        {name: 'Daniel'}
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
      this.$refs.selected.addEventListener('mousedown', function(e){ e.preventDefault(); }, false)
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
        this.users.map(user => this.selectedUsers.push(user.name))
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
    }
  },
  computed: {
    searchedUsers() {
      return this.users.filter(user => {
        return user.name
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
  padding: 12px;
  width: 265px;
  background: white;
  position: relative;
  z-index: 2;
}
.s-selected img {
  transition: transform 0.25s ease-in-out;
}
.s-modal {
  border: 1px solid blue;
  border-radius: 3px;
  padding: 12px;
  width: 265px;
  margin-top: 5px;
  opacity: 0;
  position: absolute;
  top: -5px;
  transition: all 0.5s;
  z-index: -1;
  background: white;
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
</style>