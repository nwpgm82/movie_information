<template>
<div class="search_bar">
    <a-input-search placeholder="Search movie name" enter-button @search="onSearch" class="search_icon" style="width:536px;height:48px;" />
</div>
</template>

<script>
export default {
    methods: {
        onSearch(value) {
            console.log(value);
            this.$router.push('/page/search/' + value +'?page=1')
        },

    },
}
</script>

<style scoped>
.search_bar {
    padding: 32px;
    display: flex;
    justify-content: flex-end;
    height: auto;
}

input {
    color: white;
}
</style>

