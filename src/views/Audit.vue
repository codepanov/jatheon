<template>
  <div id="audit">
    <header class="header">
      <div class="s-search">
        <input type="text" placeholder="Search for a word or phrase">
        <img 
          src="@/assets/search.svg" 
          alt="Search"
          class="icon-search"
        >
      </div>
      <Initials />
    </header>
    <section>
      <Selector :payload="users" @disable="disable" />
      <Disabled :payload="actions" v-if="disabled" />
      <Selector :payload="actions" v-else />
      <FilterInput @filter="button_active" />
      <button :class="{'button-active': filter_button}">Search Now</button>
    </section>
    <article>
      <img 
        src="@/assets/img-audit-noresults.png" 
        alt="Empty"
      >
      <p><b>Nothing to Show</b></p>
      <p>To see audit logs, choose the filters and/or<br> perform a search from the above menu.</p>
    </article>
  </div>
</template>

<script>
import Initials from '@/components/Initials.vue'
import Selector from '@/components/Selector.vue'
import Disabled from '@/components/Disabled.vue'

import FilterInput from '@/components/Filter_input.vue'
import users from '@/data/users.json'
import actions from '@/data/actions.json'

export default {
  components: {
    Initials,
    Selector,
    Disabled,
    FilterInput
  },
  data() {
    return {
      users,
      actions,
      disabled: true , // disables/enables second drop down
      filter_button: false // disables/enables filter button
    }
  },
  methods: {
    disable(value) {
      this.disabled = value
    },
    button_active(value) {
      this.filter_button = value
    }
  }
}
</script>

<style scoped>
#audit {
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  height: 100vh;
  width: 100%;
  background: #F4F4F4;
}
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;;
  background-color: #FFF;
  width: 100%;
  height: 60px;
  border-bottom: 1px solid #CFCFCF;
  box-sizing: border-box;
  padding: 0 20px;
  /* position: relative; */
}
header input {
  width: 515px;
  height: 16px;
}
header input:focus {
  outline-color: #00A88D;
}
section {
  background-color: #FFF;
  width: 100%;
  height: 70px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #CFCFCF;
  box-sizing: border-box;
  padding-left: 5px;
}
article {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #3E4543;
}
article p:nth-child(3) {
  color: #3E4543;
  font-size: 14px;
  margin-top: 0;
}
button {
  background-color: #CFCFCF;
  color: #9B9B9B;
  font-family: 'Open Sans';
  font-weight: 600;
  border-radius: 4px;
  margin-left: 15px;
  border: none;
  padding: 9px 20px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 14px;
}
button:hover {
  cursor: pointer;
}
button:focus {
  outline: none;
}
.button-active:active {
  background-color: #00725f;
}
.button-active {
  background-color: #00A88D;
  color: white;
}
</style>