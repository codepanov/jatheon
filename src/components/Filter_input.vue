<template>
  <div class="s-search filter">
    <input
      type="text"
      placeholder="Filter results..."
      v-model="filter"
      style="background: white; padding-left: 10px"
    >
    <!-- <img 
      src="@/assets/search.svg" 
      alt="Search"
      class="icon-search"
    > -->
    <img 
      src="@/assets/icn-close.svg" 
      alt="Close"
      class="icon-close"
      @click="reset_filter" 
      v-show="filter != ''" 
    >
  </div>
</template>

<script>
export default {
  data() {
    return {
      filter: ''
    }
  },
  methods: {
    reset_filter() {
      this.filter = ''
      this.$emit('filter', false)
    }
  },
  watch: {
    filter() {
      if(this.filter != '')
        this.$emit('filter', true)
      else
        this.$emit('filter', false)
      // console.log(this.filter)
    }
  }
}
</script>

<style>
::-webkit-input-placeholder { /* Chrome/Opera/Safari */
  font-size: 14px;
}
::-moz-placeholder { /* Firefox 19+ */
  font-size: 14px;
}
.filter {
  margin-left: 15px;
  border: 1px solid lightgrey;
  border-radius: 4px;
}
.filter:hover {
  border: 1px solid #00A88D;
}
.filter:focus {
  outline-color: #00A88D;
}
</style>