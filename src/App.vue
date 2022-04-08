<template> 
  <Header title="States" @update-search="searchText = $event"/>
  <main>
    <div class="container my-5">
      <div class="row align-items-start">
        <div class="col">
          <StateList :states="states" @dblclick-state="HighlightState" @click-state="showStateDetails"/>
        </div>
        <div class="col">
          <StateList :states="states" :searchText="searchText"  @dblclick-state="HighlightState" @click-state="showStateDetails"/>
        </div>
        <div v-show="stateDetail.state" class="col" >
          <StateDetail :state="stateDetail"/>
        </div>
      </div>
    </div>
  </main>
  <Footer />
</template>

<script>

import Header from './components/Header'
import StateList from './components/StateList'
import StateDetail from './components/StateDetail'
import Footer from './components/Footer'
export default {
   name: 'App',
  components: {
    Header,
    StateList,
    StateDetail,
    Footer
  },
  data() {
    return {
      states: [],
      stateDetail: {},
      searchText: ''
    }
  },
   methods: {
     async fetchStates() {
      const res = await fetch('http://pos.idtretailsolutions.com/countytest/states')
      const json = await res.json()
      return json.data
    },
    async fetchStateDetails(url) {
      const res = await fetch(url)
      const json = await res.json()
      return json.data
    },
    HighlightState(state){
      this.states  = this.states.map((s) =>
        s.state === state ? { ...s , active: !s.active } : s
      )
    },
    async showStateDetails(state){
      const _details = await this.fetchStateDetails(state.detail)
      this.stateDetail = {...state , details: _details}
    }
   },
  async created() {
     this.states = await this.fetchStates()
  },
   
}
</script>

<style scoped>
  .col{
    height: 65vh;
    overflow-y: auto;
  }
</style>

