<template>
    <div class="list-group" >
        <a v-for="st in filteredStates" :key="st.state" @dblclick="$emit('dblclick-state', st.state)" 
        @click="$emit('click-state', st)" href="#" 
        :class="[st.active ? 'active': '', 'list-group-item', 'list-group-item-action']">
        {{st.state}}</a>
    </div>
</template>

<script>
export default {
    name: 'StateList',
    props: {
        states: Array,
        searchText: {
            type: String,
            default: ''
        }
    },
    computed: {
        filteredStates(){
                return this.states.filter((state) => state.state.toLowerCase().includes(this.searchText.toLowerCase()))
        },
    }
}
</script>