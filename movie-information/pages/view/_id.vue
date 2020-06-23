<template>
<div>
    <!-- <p>{{movieDetail}}</p> -->
    <div class="box">
        <div class="movie">
            <a-row>
                <a-col :xxl="8">
                    <img class="poster" :src="`https://image.tmdb.org/t/p/w400${movieDetail.poster_path}`" alt="">
                </a-col>
                <a-col :xxl="12">
                    <div class="right_box">
                        <p class="title">{{movieDetail.title}}</p>
                        <div  style="display:flex">
                            <p v-for="i in movieDetail.genres" :key="i.id" class="category">{{i.name}} /</p>
                        </div>
                        
                    </div>
                </a-col>
            </a-row>
        </div>
    </div>

    <!-- :style="{background : `url(https://image.tmdb.org/t/p/original/${movieDetail.backdrop_path})`}" -->
    <!-- {{this.$route.params.id}}
    <p style="color:white">{{movieDetail.poster_path}}</p> -->
</div>
</template>

<script>
import axios from 'axios';
export default {
    layout: 'main',
    data() {
        return {
            movieDetail: {},
            videoDetail: {},
            key: ''
        }
    },
    async mounted() {
        await axios
            .get(`https://api.themoviedb.org/3/movie/${this.$route.params.id}?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)
            .then(response => {
                this.movieDetail = response.data
                console.log('Current page : ', this.current)
            })
            .catch(err => {
                console.log(err)
            })
        await axios
            .get(`https://api.themoviedb.org/3/movie/${this.$route.params.id}/videos?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)
            .then(response => {
                this.videoDetail = response.data
                console.log('Current page : ', this.current)
            })
            .catch(err => {
                console.log(err)
            })
        this.key = await this.videoDetail.results[0].key
    },
}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

/* .bg {
    position: relative;
    width: 100%;
    height: 550px;
    -o-object-fit: cover;
    object-fit: cover;
    background-size: cover;
    opacity: 0.2;
    -webkit-mask-image: -webkit-gradient(linear, left top, left bottom, from(rgba(0, 0, 0, 1)), to(rgba(0, 0, 0, 0)));
    mask-image: linear-gradient(to bottom, rgba(0, 0, 0, 1), rgba(0, 0, 0, 0));
} */

.box {
    margin-top: 250px;
    transition: 0.3s;
    width: 976px;
    height: 496px;
    margin: auto;
}

.movie {
    display: block;
    margin: auto;
    width: 976px;
    height: 496px;
    transition: 0.3s;
}

.right_box {
    width: 648px;
    height: 496px;
    padding: 32px;
    background: rgba(0, 0, 0, 0.25);
}

.title {
    font-style: normal;
    font-weight: 800;
    font-size: 44px;
    line-height: 56px;
    letter-spacing: 0.08em;
    text-transform: uppercase;

    color: #FFFFFF;

}

.category {
    margin-right: 8px;
    font-style: normal;
    font-weight: 600;
    font-size: 24px;
    line-height: 29px;
    /* identical to box height */
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #FFFFFF;
}

/* .box:hover .movie {
    opacity: 0;
} */

p {
    color: white;
}

.poster {
    width: 100%;
    height: 496px;
}
</style>
