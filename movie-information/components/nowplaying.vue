<template>
<div class="nowplaying">
    <div class="topic_box">
        <p class="topic">now playing</p>
    </div>
    <div class="box">
        <a-row class="row">
            <a-col :xs="12" :sm="12" :md="8" :lg="6" :xl="6" :xxl="6" v-for="i in nowplaying.results" :key="i.id">
                <div class="card">
                    <a :href="`/page/detail/${i.id}`">
                        <img v-if="i.poster_path" :src="`https://image.tmdb.org/t/p/original/${i.poster_path}`" :alt="i.title" class="movie_img">
                        <img v-if="i.poster_path == null" class="movie_img" src="https://upload.wikimedia.org/wikipedia/commons/f/fc/No_picture_available.png" alt="">
                        <p class="movie_topic">{{i.title}}</p>
                        <p class="movie_date">{{formatDate(i.release_date)}}</p>
                        <div class="circle_box">
                            <a-progress class="nowshowing-progress" type="circle" :percent="`${i.vote_average}`*10" :stroke-width="10" :strokeColor="setColor(i.vote_average)" :width="40" />
                        </div>
                    </a>
                </div>
            </a-col>
        </a-row>
        <!-- <a href="" class="see">See More movies</a> -->
    </div>
</div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'
export default {
    data() {
        return {
            nowplaying: {}
        }
    },
    methods: {
        formatDate(date) {
            return moment(date).format('DD MMMM YYYY')
        },
        setColor(i) {
            // console.log(i)
            var code = ""
            if (i <= 10) {
                code = "1FDC54"
            }
            if (i <= 6.5) {
                code = "FAAC14"
            }
            if (i <= 3.5) {
                code = "E12626"
            }
            return code;
        }
    },
    mounted() {
        axios
            .get(`https://api.themoviedb.org/3/movie/now_playing?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US&page=1`)

            .then(response => {
                this.nowplaying = response.data
                // console.log(this.box)
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

.nowplaying {
    padding: 0px 0px 64px 0px;
}

.topic_box {
    width: 994px;
    height: 64px;
    margin: auto;
    padding: 20px 24px;
    background: #FADB14;
    border-radius: 5px 5px 0px 0px;
}

.topic {
    font-style: normal;
    font-weight: bold;
    font-size: 24px;
    line-height: 24px;
    /* or 133% */

    display: flex;
    align-items: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #262626;
}

.box {
    width: 1152px;
    height: 2128px;
    margin: auto;
    padding: 0 24px;
    border-radius: 0 0 5px 5px;
}

.row {
    margin: 16px auto;
    width: 960px;
}

.card {
    margin: 24px auto 0 auto;
    width: 208px;
    height: 360px;
    padding: 8px;
    background: #262626;
    border-radius: 5px;
    transition: 0.3s;
    cursor: pointer;
}

.card:hover {
    background: rgba(250, 219, 20, 1);
}

/* .card:hover .movie_img {
    -webkit-mask-image: -webkit-gradient(linear, left top, left bottom, from(rgba(250, 219, 20, 1)), to(rgba(250, 219, 20, 0.1)));
    mask-image: linear-gradient(to bottom, rgba(250, 219, 20, 1), rgba(250, 219, 20, 0));
} */

.card:hover .movie_topic {
    color: #262626;
}

.card:hover .movie_date {
    color: #262626
}

.movie_img {
    width: 192px;
    height: 288px;
    border-radius: 5px;
    transition: 0.3s;
    position: relative;
}

.movie_topic {
    margin-top: 8px;
    font-style: normal;
    font-weight: bold;
    font-size: 20px;
    text-align: center;
    letter-spacing: 0.04em;
    line-height: 22px;
    text-transform: uppercase;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    color: #FFFFFF;

}

.movie_date {
    font-style: normal;
    font-weight: normal;
    font-size: 14px;
    text-align: center;
    letter-spacing: 0.14em;
    line-height: 22px;
    text-transform: uppercase;

    color: #FFFFFF;
}

.circle_box {
    position: absolute;
    top: 8px;
    right: -2px;
}

.see {
    margin: 32px 0;
    font-style: normal;
    font-weight: bold;
    font-size: 24px;
    line-height: 32px;
    display: flex;
    justify-content: flex-end;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    text-decoration-line: underline;
    color: #262626;
}

.ant-progress {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    color: rgba(0, 0, 0, 0.65);
    font-size: 14px;
    font-variant: tabular-nums;
    line-height: 1.5;
    list-style: none;
    font-feature-settings: 'tnum', "tnum", "tnum";
    display: inline-block;
    background: azure;
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background-color: #262626;
}

@media screen and (max-width: 1199px) {
    .box {
        width: 100%;
        height: 100%;
    }

    .row {
        width: 100%;
        height: 100%;
    }

    .topic_box {
        width: 95%;
    }
}

@media screen and (max-width: 767px) {
    .box{
        padding: 0 12px;
    }
    .topic_box {
        width: 90%;
    }

    .card {
        width: 150px;
        height: 264px;
    }

    .movie_img {
        width: 136px;
        height: 204px;
    }

    .movie_topic {
        margin-top: 4px;
        font-size: 20px;
    }

    .movie_date {
        font-size: 14px;
        letter-spacing: 0.08em;
    }
}

@media screen and (min-width: 400px) and (max-width: 414px) {
    .circle_box {
        right: 4px;
    }
}

@media screen and (max-width: 399px) {
    .circle_box {
        right: -8px;
    }
}

@media screen and (max-width: 320px) {
    .box {
        padding: 10px;
    }

    .topic_box {
        margin-top: 32px;
        height: 68px;
    }

    .topic {
        font-size: 28px !important;
    }
    .card{
        width: 132px;
        height: 244px;
    }

    .movie_img{
        width: 116px;
        height: 184px;
    }
}
</style><style>
.nowshowing-progress .ant-progress-text {
    font-size: 14px;
}
</style>
