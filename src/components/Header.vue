<template>
    <header>
        <nav class="navbar navbar-light bg-light">
            <div class="container-fluid d-flex justify-content-around">
                <a class="navbar-brand">{{ title }}</a>
                <Search @update-search="$emit('update-search', $event)"/>
            </div>
        </nav>
    </header>
</template>

<script>
import Search from './Search'

export default{
    name:'Header',
    props: {
        title: String
    }, components: {
        Search
    },
    emits: ['update-search']
}
</script>


