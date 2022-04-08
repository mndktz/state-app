<template>
     <div class="list-group list-group-flush" >
        <li class="list-group-item">
            <span class="fw-bold">Name:</span> {{state.state}} 
        </li>
        <li class="list-group-item"> 
            <span class="fw-bold">Population:</span> {{state.population}} 
        </li>
        <li class="list-group-item" v-if="state.details"> 
            <span class="fw-bold">Number of Counties:</span> {{state.details.length}}
        </li>
        <span class="fw-bold ms-3 my-2">Counties:</span>
            
            <ul v-if="state.details" class="list-group list-group-item list-group-flush inner-list">
                
                <li  v-for="detail in state.details" :key="detail.county" class="list-group-item">
                    <div class="ms-2 me-auto">
                        <div class="fw-bold">{{detail.county}}</div>
                        Population {{detail.population}}
                    </div>
                </li>
            </ul>
            <li v-if="state.details" class="list-group-item">
                <span class="fw-bold">Total County Population:</span> {{sumCountiesPopulation}} 
            </li>
            <li v-if="state.details" class="list-group-item">
                <span class="fw-bold">Total County Equals Total State:</span> <i :class="[totalsAreCompatible ? 'fa-check text-success': 'fa-x text-danger','fa-solid', 'ms-2']"></i>
            </li>
    </div>
</template>
<script>
export default {
    data(){
        return{
            sumCountiesPopulation: Number,
            totalsAreCompatible: Boolean
        }
    },
    name: 'StateDetail',
    props: {
        state: Object
    },
     watch: { 
      	state() {
          this.sumCountiesPopulation  = this.state.details.reduce((acc, detail) =>
                acc  + detail.population
          , 0)
            this.totalsAreCompatible = this.state.population === this.sumCountiesPopulation;
        }
     }
}
</script>

<style scoped>
    .inner-list{
        max-height: 33vh;
        overflow-y: auto;
    }
</style>