<template>
<div>
    <search />
    <upcoming />
    <div style="background:rgba(38, 38, 38, 0.65);">
        <toprated/>
    <popular/>
    <nowplaying/>
    </div>
    
</div>
</template>

<script>
import axios from 'axios';
import search from '@/components/search'
import upcoming from '@/components/upcoming'
import toprated from '@/components/toprated'
import popular from '@/components/popular'
import nowplaying from '@/components/nowplaying'
export default {
    layout: 'main',
    components: {
        search,
        upcoming,
        toprated,
        popular,
        nowplaying
    },
    data() {
        return {
            post: {},
        }
    },
    methods: {

        // this.$router.push('/page/' + this.current)
    },
    // mounted() {
    //     axios
    //         .get(`https://api.themoviedb.org/3/discover/movie?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=${this.current}`)

    //         .then(response => {
    //             this.post = response.data
    //             console.log(this.current)
    //         })
    //         .catch(err => {
    //             console.log(err)
    //         })
    // }

}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}


</style>
