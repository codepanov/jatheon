<template>
  <div class="circle">
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
      <!-- Left this comment here as a reminder taht those should be links to their respective routes -->
      <!-- <router-link to="#">Account Settings</router-link> -->
      <p class="acc-bottom">Account Settings</p>
      <p class="acc-bottom">Company Settings</p>
      <p class="acc-bottom">Help Center</p>
      <p class="acc-bottom">Log Out</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      expanded: false,
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

<style>
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
  /* right: 20px; */
  transition: all 0.5s;
}
.circle-initials-expanded {
  background: #CBEDE8;
  color: #00A88D;
}
/* Added one rule */
/* .s-modal {
  right: 20px;
} */
/* Added one rule */
/* .s-modal-expanded {
  right: 20px;
} */
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
.audit {
  letter-spacing: 0.3px;
  right: 20px;
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
.header-right {
  display: flex;
  cursor: pointer;
}
.header-right img {
  transition: transform 0.25s ease-in-out;
}
@media screen and (max-width: 1170px) {
  .audit {
    top: 114px!important;
  }
}
</style>