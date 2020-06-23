<template>
<div style="padding:54px;">
    <div class="box">
        <div class="topic_box">
            <p>popular movies</p>
        </div>
        <div>
            <a-row class="row">
                <a-col :md="16" :xl="16" :xxl="16">
                    <a :href="`/page/detail/${popular.id}`">
                        <div class="popular_box">
                            <img v-if="popular.backdrop_path" :src="`https://image.tmdb.org/t/p/original${popular.backdrop_path}`" alt="" class="first_popular">
                            <img v-if="popular.backdrop_path == null" src="https://upload.wikimedia.org/wikipedia/commons/f/fc/No_picture_available.png" alt="" class="first_popular">
                            <div class="popular_title_box">
                                <p class="popular_topic">{{popular.title}}</p>
                                <p class="popular_date">{{formatDate(popular.release_date)}}</p>
                            </div>
                            <div class="fade_shadow"></div>
                            <div style="position:absolute;top:8px;right:8px">
                                <a-progress type="circle" :percent="`${popular.vote_average}`*10" :stroke-width="10" :strokeColor="setColor(popular.vote_average)" :width="64" />
                            </div>

                            <!-- <p style="color:white">{{popular}}</p> -->
                        </div>
                    </a>
                </a-col>
                <a-col :md="8" :xl="8" :xxl="8" v-for="j in box" :key="j.id">
                    <a :href="`/page/detail/${j.id}`">
                        <div class="popular_box">
                            <img v-if="j.backdrop_path" :src="`https://image.tmdb.org/t/p/original${j.backdrop_path}`" alt="">
                            <img v-if="j.backdrop_path == null" src="https://upload.wikimedia.org/wikipedia/commons/f/fc/No_picture_available.png" alt="">
                            <div class="popular_title_box">
                                <p class="popular_topic">{{j.title}}</p>
                                <p class="popular_date">{{formatDate(j.release_date)}}</p>
                            </div>
                            <div class="fade_shadow"></div>
                            <div style="position:absolute;top:8px;right:8px">
                                <a-progress type="circle" :percent="`${j.vote_average}`*10" :stroke-width="10" :strokeColor="setColor(j.vote_average)" :width="64" />
                            </div>
                            <!-- <p style="color:white">{{box}}</p> -->
                        </div>
                    </a>
                </a-col>
            </a-row>
        </div>
    </div>
    <!-------------mobile--------------->
    <div class="mobile">
        <div class="mobile_topic_box">
            <p class="mobile_topic">Popular Movies</p>
        </div>
        <a-row class="mobile_card">
            <a :href="`/page/detail/${popular.id}`">
                <a-col :xs="8">
                    <div>
                        <img v-if="popular.backdrop_path" :src="`https://image.tmdb.org/t/p/original${popular.backdrop_path}`" alt="" class="mobile_img">
                        <img v-if="popular.backdrop_path == null" src="https://upload.wikimedia.org/wikipedia/commons/f/fc/No_picture_available.png" alt="" class="mobile_img">
                    </div>
                </a-col>
                <a-col :xs="10" style="padding:20px 6px !important">
                    <div>
                        <p class="popular_topic">{{popular.title}}</p>
                        <p class="popular_date">{{formatDate(popular.release_date)}}</p>
                    </div>
                </a-col>
                <a-col :xs="6">
                    <div>
                        <a-progress type="circle" :percent="`${popular.vote_average}`*10" :stroke-width="10" :strokeColor="setColor(popular.vote_average)" :width="64" style="margin:auto;display:block" />
                    </div>
                </a-col>
            </a>
        </a-row>
        <a-row class="mobile_card" v-for="j in box" :key="j.id">
            <a :href="`/page/detail/${j.id}`">
                <a-col :xs="8" :sm="8">
                    <div>
                        <img v-if="j.backdrop_path" :src="`https://image.tmdb.org/t/p/original${j.backdrop_path}`" alt="" class="mobile_img">
                        <img v-if="j.backdrop_path == null" src="https://upload.wikimedia.org/wikipedia/commons/f/fc/No_picture_available.png" alt="" class="mobile_img">
                    </div>
                </a-col>
                <a-col :xs="10" :sm="10" style="padding:20px 6px !important">
                    <div>
                        <p class="popular_topic">{{j.title}}</p>
                        <p class="popular_date">{{formatDate(j.release_date)}}</p>
                    </div>
                </a-col>
                <a-col :xs="6" :sm="6">
                    <div>
                        <a-progress type="circle" :percent="`${j.vote_average}`*10" :stroke-width="10" :strokeColor="setColor(j.vote_average)" :width="64" style="margin:auto;display:block" />
                    </div>
                </a-col>
            </a>
        </a-row>
    </div>
</div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'
export default {
    data() {
        return {
            popular: [],
            box: []
        }
    },
    methods: {
        formatDate(date) {
            return moment(date).format('DD MMMM YYYY')
        },
        setColor(j) {
            // console.log(j)
            var code = ""
            if (j <= 10) {
                code = "1FDC54"
            }
            if (j <= 6.5) {
                code = "FAAC14"
            }
            if (j <= 3.5) {
                code = "E12626"
            }
            return code;
        }
    },
    mounted() {
        axios
            .get(`https://api.themoviedb.org/3/movie/popular?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)

            .then(response => {
                this.popular = response.data.results[0]
                var i
                for (i = 1; i <= 5; i++) {
                    if (i === 1) {
                        continue;
                    }
                    this.box.push(response.data.results[i - 1])
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

.box {
    margin: auto;
    width: 960px;
    height: auto;
    background: #262626;
    border-radius: 5px;
}

.topic_box {
    width: 960px;
    height: 88px;
    font-style: normal;
    font-weight: bold;
    font-size: 44px;
    line-height: 32px;
    /* or 73% */
    text-align: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FADB14;
    padding: 26px 0;
}

.row {
    width: 960px;
    height: 100%;
}

/* .popular_box{
    transition: 1s;
} */

/* .popular_box:hover{
    transform: scale(1.01);
    z-index: 999;
}  */

.fade_shadow {
    width: 100%;
    height: 424px;
    position: absolute;
    padding: 24px;
    bottom: 0px;
    left: 0px;
    transition: 0.3s;
    background: transparent;
    opacity: 0;
    cursor: pointer;
}

.popular_box:hover .fade_shadow {
    opacity: 1;
    background: linear-gradient(180deg, rgba(38, 38, 38, 0) 0%, #262626 94.35%);
}

.first_popular {
    width: 640px;
    height: 424px;
    object-fit: cover;
    position: relative;
}

img {
    width: 320px;
    height: 424px;
    object-fit: cover;
}

.popular_title_box {
    width: 100%;
    position: absolute;
    bottom: 24px;
    left: 24px;
    z-index: 2;

}

.popular_topic {
    width: 250px;
    height: auto;
    font-style: normal;
    font-weight: 600;
    font-size: 24px;
    line-height: 29px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #FFFFFF;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.popular_date {
    font-style: normal;
    font-weight: 500;
    font-size: 20px;
    line-height: 24px;
    /* identical to box height */

    display: flex;
    align-items: center;
    text-transform: uppercase;

    color: #FFFFFF;
}

.mobile {
    margin-top: 64px;
    width: 100%;
    display: none;
}

.mobile_topic_box {
    width: 90%;
    height: 70px;
    margin: auto;
    border-radius: 5px;
    background: #262626;

}

.mobile_topic {
    font-style: normal;
    font-weight: bold;
    font-size: 28px;
    line-height: 32px;
    /* or 73% */
    text-align: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FADB14;
    padding: 18px 0;
}

.mobile_card {
    width: 90%;
    height: 104px;
    border-radius: 5px;
    padding: 0;
    background: #262626;
    margin: 16px auto;
}

.mobile_img {
    width: 120px;
    height: 104px;
    object-fit: cover;
    object-position: center;
    border-radius: 5px 0 0 5px;
}

@media screen and (max-width: 1024px) {

    .box,
    .topic_box,
    .row,
    img {
        width: 100%;
    }

    .popular_topic {
        width: 180px;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .popular_date {
        width: 100%;
    }
}

@media screen and (max-width: 767px) {
    div {
        padding: 0px !important;
    }

    .box {
        display: none;
    }

    .mobile {
        display: block;
    }

    .popular_topic {
        font-size: 18px;
        white-space: nowrap;
        width: 102px;
        overflow: hidden;
        text-overflow: ellipsis;

    }

    .popular_date {
        font-size: 16px;
    }
     .ant-progress{
       top: 16px;
       right: 8px;
   }
}

@media screen and (max-width: 360px){
    .mobile_img{
        width: 100%;
    }
}

@media screen and (max-width: 320px) {
  
    .mobile_img {
        width: 90%;
    }

    .popular_topic {
        font-size: 16px;
    }

    .popular_date {
        font-size: 14px;
    }
}
</style>
