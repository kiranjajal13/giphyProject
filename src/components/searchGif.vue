<template>
    <div>
        <input class="searchBar" placeholder="Search to get amazing gifs!" v-model="keyword"/>
        <button @click="onSearch">Search</button>
    </div>
</template>
<script>
export default {
    data() {
        return {
            keyword: ''
        }
    },
    methods: {
        onSearch() {
            this.$emit('gifKeyword', this.keyword)
        }
    }

}
</script>
<style>
.searchBar {
    border: 1px solid black;
    width: 70%;
    height: 50px;
}
</style>