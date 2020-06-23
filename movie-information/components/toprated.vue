<template>
<div>
    <div class="toprated">
        <div style="padding: 32px 56px 0px 56px;">
            <div >
                <img src="~/assets/img/toprated.png" alt="" class="topic_arrow">
                <img src="~/assets/img/toprated_mobile.png" alt="" class="topic_arrow_mobile">
                <p class="topic">TOP RATED MOVIE</p>
            </div>
            <!-- <a href="" class="see">SEE MORE MOVIES</a> -->
        </div>
        <div>
            <div class="movie">
                <div v-for="i in box" :key="i.id">
                    <a :href="`/page/detail/${i.id}`">
                        <div class="card1">
                            <img :src="`https://image.tmdb.org/t/p/original/${i.poster_path}`" alt="" class="movie_card">
                            <div style="position:absolute;bottom:24px;left:16px;right:16px">
                                <p class="card_title">{{i.title}}</p>
                                <p class="card_release_date">{{formatDate(i.release_date)}}</p>
                            </div>

                            <div style="position:absolute;top:8px;right:4px">
                                <a-progress type="circle" :percent="`${i.vote_average}`*10" :stroke-width="10" :strokeColor="setColor(i.vote_average)" :width="64" />
                            </div>
                        </div>
                    </a>

                </div>
            </div>
        </div>

    </div>
    <p></p>
</div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'
export default {
    data() {
        return {
            toprated: {},
            box: []
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
            .get(`https://api.themoviedb.org/3/movie/top_rated?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)

            .then(response => {
                this.toprated = response.data
                var i
                for (i = 1; i <= 10; i++) {
                    this.box.push(this.toprated.results[i - 1])
                }
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

.toprated {
    height: 100%;
    position: relative;
}

.topic_arrow {
    position: relative;
    top: 0px;
    left: -56px;
}

.topic_arrow_mobile {
    display: none;
    position: relative;
    top: 0px;
    left: -56px;
}

.topic {
    font-style: normal;
    font-weight: bold;
    font-size: 44px;
    line-height: 32px;
    /* or 73% */

    display: flex;
    align-items: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #262626;

    position: absolute;
    top: 58px;
    left: 48px;
}

.see {
    font-style: normal;
    font-weight: 600;
    font-size: 24px;
    line-height: 29px;
    /* identical to box height */

    display: flex;
    align-items: center;
    letter-spacing: 0.08em;
    text-decoration-line: underline;
    text-transform: uppercase;

    color: #FFFFFF;

}

.movie {
    margin-top: 54px;
    padding: 10px 0 20px 32px;
    display: flex;
    overflow-x: scroll;
    overflow-y: hidden;
    white-space: nowrap;
}

::-webkit-scrollbar {
    width: 10px;
    height: 5px;

}

::-webkit-scrollbar-track {
    background: none;
    border-radius: 10px;
}

::-webkit-scrollbar-thumb {
    background: #FADB14;
    border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
    background: #d6bc13;
}

div.movie a {
    display: inline-block;
    color: white;
    text-align: center;
    /* padding: 14px; */
    text-decoration: none;
}

.card1 {
    width: 304px;
    height: 456px;
    border-radius: 5px;
    position: relative;
    display: inline-block;
    vertical-align: top;
    margin-right: 48px;
    margin-bottom: 10px;
    cursor: pointer;
    transition: 0.3s;
}

.movie_card {
    width: 304px;
    height: 456px;
    overflow: hidden;
    border-radius: 5px;
    -webkit-mask-image: -webkit-gradient(linear, left top, left bottom, from(rgba(38, 38, 38, 1)), to(rgba(38, 38, 38, 0)));
}

.card1:hover {
    transform: scale(1.04);
    box-shadow: 0px 8px 12px #0D0D0D;
    background: linear-gradient(180deg, rgba(13, 13, 13, 0) 0%, #0D0D0D 94.35%);
}

.card_title {
    font-style: normal;
    font-weight: 600;
    font-size: 24px;
    line-height: 29px;
    text-align: center;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #FFFFFF;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;

}

.card_release_date {
    font-style: normal;
    font-weight: normal;
    font-size: 20px;
    line-height: 24px;
    /* identical to box height */
    text-align: center;
    text-transform: uppercase;

    color: #FFFFFF;

}

@media screen and (max-width: 767px) {
    .topic_arrow {
        display: none;
    }

    .topic_arrow_mobile {
        display: block;
    }

    .topic {
        top: 58px;
        left: 8px;
    }

    .card1 {
        width: 200px;
        height: 300px;
    }

    .movie_card {
        width: 200px;
        height: 300px;
    }

    .card_title {
        font-size: 20px;
    }

    .card_release_date {
        font-size: 16px;
    }
}
</style><style>
.card1 .ant-progress-circle .ant-progress-inner {
    position: relative;
    line-height: 1;
    background-color: #262626;
    top: 4px;
    left: 1px;
}

@media screen and (max-width: 767px) {
    .card1 .ant-progress-circle .ant-progress-inner {
        top: 4px;
        left: 0px;
    }
}

@media screen and (max-width: 320px){
    .topic_arrow_mobile{
        width: 290px;
    }
    .topic{
        font-size: 36px !important;
        top: 50px !important;
    }
}
</style>
