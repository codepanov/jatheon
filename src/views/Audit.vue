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
      <div class="header-right" @click="expand()" ref="initials">
        <div class="circle-initials" :class="{'circle-initials-expanded': expanded}">
          <span><b>JD</b></span>
        </div>
        <img src="@/assets/icn-arrow-down.svg" alt="Arrow" ref="image">
      </div>
      <div class="s-modal audit" :class="{'s-modal-expanded': expanded}">
        <p>Administrator</p>
        <p>john.doe@jatheon.com</p>
        <p>Jatheon Technologies</p>
        <div class="separator"></div>
        <!-- Left here as a reminder taht those should be links to their respective routes -->
        <!-- <router-link to="#">Account Settings</router-link> -->
        <p class="acc-bottom">Account Settings</p>
        <p class="acc-bottom">Company Settings</p>
        <p class="acc-bottom">Help Center</p>
        <p class="acc-bottom">Log Out</p>
      </div>
    </header>
    <section>
      <Selector />
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
import Selector from '@/components/Selector.vue'

export default {
  components: {
    Selector
  },
  data() {
    return {
      expanded: false
    }
  },
  methods: {
    expand() {
      let refs = [this.$refs.initials] // left in an array for future added elements
      refs.map(ref => ref.addEventListener('mousedown', function(e){ e.preventDefault() }, false))
      if(!this.expanded)
        this.$refs.image.setAttribute('style', `transform: rotateZ(180deg)`)
      else
        this.$refs.image.setAttribute('style', `transform: rotateZ(0deg)`)
      this.expanded = !this.expanded
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
.header-right {
  display: flex;
  cursor: pointer;
}
.header-right img {
  transition: transform 0.25s ease-in-out;
}
.circle-initials {
  background: #F4F4F4;
  border-radius: 100%;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 5px;
  color: #9B9B9B;
  font-size: 12px;
  padding: 0px 0 2px 2px;
  box-sizing: border-box;
  transition: all 0.5s;
}
.circle-initials-expanded {
  background: #CBEDE8;
  color: #00A88D;
}
/* Added one rule */
.s-modal {
  right: 20px;
}
/* Added one rule */
.s-modal-expanded {
  right: 20px;
}
.audit {
  letter-spacing: 0.3px;
}
.s-modal p:first-child {
  text-transform: uppercase;
  color: #9B9B9B;
  font-size: 11px;
  line-height: 18px;
  font-weight: bolder;
  margin: 0;
}
.s-modal p:nth-child(2) {
  color: #3E4543;
  font-size: 14px;
  line-height: 18px;
  margin: 5px 0 0 0;
  font-weight: bolder;
}
.s-modal p:nth-child(3) {
  color: #3E4543;
  font-size: 14px;
  line-height: 18px;
  margin: 5px 0 0 0;
}
.separator {
  background-color: #CFCFCF;
  height: 1px;
  margin: 10px 0;
}
.acc-bottom {
  color: #3E4543;
  font-size: 14px;
  line-height: 18px;
  margin: 10px 0 0 0;
  cursor: pointer;
}
.acc-bottom:hover {
  color: #00A88D;
}
section {
  background-color: #FFF;
  width: 100%;
  height: 70px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #CFCFCF;
  box-sizing: border-box;
  padding-left: 20px;
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
</style>