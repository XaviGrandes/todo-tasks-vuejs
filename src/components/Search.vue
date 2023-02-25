<template>
    <div id="search-container">
        <input class="input" type="text" placeholder="Search task" v-model="query" v-on:input="$emit('query-change', query)"/>
    </div>
</template>

<script>
export default {
    name: 'Search',
    data() {
        return{
            query: ''
        }
    }
}
</script>

<style>
#search-container{
    width: 600px;
    margin: 0 auto;
}

.input{
    padding: 10px;
    width: 100%;
    outline: none;
}

@media only screen and (min-width: 355px) {
    #search-container{
    width: 330px;
    margin: 0 auto;
}
}

</style>