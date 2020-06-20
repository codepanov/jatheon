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
  background-color: #FFF;
  width: 100%;
  height: 60px;
  border-bottom: 1px solid #CFCFCF;
  box-sizing: border-box;
  padding-left: 20px;
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
header input {
  width: 515px;
  height: 20px;
}
header input:focus {
  outline-color: #00A88D;
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