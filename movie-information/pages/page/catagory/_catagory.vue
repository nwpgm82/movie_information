<template>
<div>
    <div class="container">
        <div style="display:flex;justify-content:space-between">
            <h1>Result search : {{this.$route.params.search}}</h1>
            <a-input-search placeholder="input search text" style="width: 200px" @search="onSearch" />
        </div>

        <a-row :gutter="[16,16]" style="margin-top:40px">
            <!-- {{post}} -->
            <a-col :xxl="4" v-for="i in post.results" :key="i.id">
                <div class="card">
                    <img v-if="i.poster_path" :src="`https://image.tmdb.org/t/p/w500/${i.poster_path}`">
                    <img v-if="i.poster_path == null" src="https://upload.wikimedia.org/wikipedia/en/6/60/No_Picture.jpg" alt="">
                    <div class="box-text">
                        <a :href="`/view/${i.id}`" class="title">{{i.original_title}}</a>
                    </div>
                </div>
            </a-col>
            <h1 id="err"></h1>
            <!-- <img v-if="i.backdrop_path" :src="`https://image.tmdb.org/t/p/original/${i.backdrop_path}`"> -->
        </a-row>
    </div>
</div>
</template>

<script>
import axios from 'axios';
export default {
    layout: 'main',
    data() {
        return {
            catagory_id: this.$route.params.catagory,
            post: []
        }
    },
    methods: {
        onSearch(value) {
            // console.log(value);
            this.$router.push('/page/search/' + value)
        },
        onChange(current) {
            this.current = current;
            // console.log('Change page to : ', this.current)
            this.$router.push('/page/' + this.current)
            if (this.current == 1) {
                this.$router.push('/')
            }
        },
        itemRender(current, type, originalElement) {
            if (type === 'prev') {
                return <a > Previous </a>;
            } else if (type === 'next') {
                return <a > Next </a>;
            }
            return originalElement;
        },
    },
    mounted() {
        axios
            .get(`https://api.themoviedb.org/3/discover/movie?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1&with_genres=${this.catagory_id}`)

            .then(response => {
                this.post = response.data
                // console.log('Current page : ', this.current)
            })
            .catch(err => {
                console.log(err)
            })
    }
}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.container {
    width: 70%;
    margin: 120px auto;
}

.card {
    width: 100%;
    height: 320px;
    background: #D19C3C;
    border-radius: 4px;
    overflow: hidden;
    padding: 4px;
}

img {
    width: 100%;
    height: 258px;
    object-fit: cover;
}

.box-text {
    padding: 10px;
    text-align: center;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    color: white;
}

h1 {
    color: white;
}

.title {
    font-size: 14px;
    color: #ffffff;
}
</style>
