<template>
    <form class="d-flex">
        <input @input="$emit('update-search', searchText)" v-model="searchText" class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
    </form>
</template>

<script>
export default {
    name: 'Search',
    data() {
        return {
            searchText: ''
        }
    }
}
</script>