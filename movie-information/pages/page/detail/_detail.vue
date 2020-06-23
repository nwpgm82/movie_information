<template>
<div style="background:rgba(38, 38, 38, 0.65);">
    <search />
    <!-- {{$route.params.detail}} -->
    <div class="overview_box">
        <img :src="`https://image.tmdb.org/t/p/original${movieDetail.backdrop_path}`" alt="" class="overview_box_backdrop">
        <a-row class="overview_box_detail">
            <a-col :xs="24" :sm="24" :md="8" :lg="9" :xl="8" :xxl="8">
                <img :src="`https://image.tmdb.org/t/p/original${movieDetail.poster_path}`" alt="" class="overview_box_poster">
            </a-col>
            <a-col :xs="24" :sm="24" :md="16" :lg="15" :xl="16" :xxl="16">
                <iframe width="760" height="520" :src="`https://www.youtube.com/embed/${videoKey}`" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
            </a-col>
        </a-row>
    </div>
    <div class="detail_box">
        <a-row class="movie_detail_box" :gutter="[0,16]">
            <a-col :md="18" :lg="17" :xl="17" :xxl="17">
                <p class="title">{{movieDetail.title}}</p>
                <div class="release_box">
                    <div class="release_date_box">
                        <p class="release_date_text">{{formatDate(movieDetail.release_date)}}</p>
                    </div>
                    <div class="release_genres">
                        <div v-for="i in movieDetail.genres" :key="i.id" style="margin-left:16px">
                            <p class="category_text">{{i.name}}</p>
                        </div>
                    </div>

                </div>
                <a-row class="rated_box">
                    <a-col :xs="5" :sm="5" :md="5" :lg="5" :xl="5" :xxl="5">
                        <a-progress class="nowshowing-progress" type="circle" :percent="`${movieDetail.vote_average}`*10" :stroke-width="10" :strokeColor="setColor(movieDetail.vote_average)" :width="64" />
                    </a-col>
                    <a-col :xs="12" :sm="12" :md="12" :lg="12" :xl="12" :xxl="12" style="padding-top:10px">
                        <div class="rectangle">
                            <a-rate :default-value="2.5" allow-half class="starIcon" />
                        </div>
                    </a-col>
                    <a-col :xs="4" :sm="4" :md="4" :lg="4" :xl="4" :xxl="4" style="padding-top:10px">
                        <div class="circle">
                            <a-icon type="heart" theme="outlined" class="icon" />
                        </div>
                    </a-col>
                    <a-col :xs="3" :sm="3" :md="3" :lg="3" :xl="3" :xxl="3" style="padding-top:10px">
                        <div class="circle">
                            <a-icon type="flag" theme="outlined" class="icon" />
                        </div>
                    </a-col>
                </a-row>
                <div class="movie_detail_text_box">
                    <p class="movie_detail_text">{{movieDetail.overview}}</p>
                </div>
                <!----director--->
                <div class="director">
                    <div v-for="(d,index) in director" :key="index" style="margin-right:40px;margin-bottom:12px">
                        <img v-if="d.profile_path" :src="`https://image.tmdb.org/t/p/original${d.profile_path}`" alt="" class="director_profile">
                        <img v-if="d.profile_path == null" :src="`https://upload.wikimedia.org/wikipedia/commons/f/fc/No_picture_available.png`" alt="" class="director_profile">
                        <div style="margin-top:8px">
                            <p class="director_name">{{d.name}}</p>
                            <p class="director_job">{{d.job}}</p>
                        </div>
                    </div>
                </div>
                <!--------------->
                <!----cast------->
                <p class="cast_topic">The Actor</p>
                <div class="cast">
                    <div v-for="(c,index) in cast" :key="index" style="margin-right:40px;margin-bottom:12px">
                        <img v-if="c.profile_path" :src="`https://image.tmdb.org/t/p/original${c.profile_path}`" alt="" class="cast_profile">
                        <img v-if="c.profile_path == null" :src="`https://upload.wikimedia.org/wikipedia/commons/f/fc/No_picture_available.png`" alt="" class="cast_profile">
                        <div class="cast_name_box">
                            <p class="cast_name">{{c.name}}</p>
                        </div>
                    </div>
                </div>
                <!--------------->
                <!----recommendation--->
                <p class="rec_topic" v-if="recommendations[0]">Recommendations</p>
                <div class="rec" v-if="recommendations[0]">
                    <div v-for="(r,index) in recommendations" :key="index" style="margin-right:40px;margin-bottom:12px">
                        <img v-if="r.poster_path" :src="`https://image.tmdb.org/t/p/original${r.poster_path}`" alt="" class="rec_img">
                        <div style="display:flex;justify-content:space-between;padding:8px">
                            <p v-if="r.title" class="rec_text">{{r.title}}</p>
                            <p v-if="r.vote_average" class="rec_text2">{{r.vote_average*10}}%</p>
                        </div>
                    </div>

                </div>
                <!--------------------->
                <comment id="a1" />
            </a-col>
            <a-col :xs="24" :sm="24" :md="6" :lg="7" :xl="7" :xxl="7">
                <div class="row">
                    <comment id="a1_2" />
                    <div class="box_detail" id="a2">
                        <div>
                            <p class="box_topic_title">{{movieDetail.original_title}}</p>
                            <p class="box_topic">Original Title</p>
                        </div>
                        <div style="margin-top:32px">
                            <p class="box_topic_title">{{movieDetail.language_name}}</p>
                            <p class="box_topic">Original Language</p>
                        </div>
                        <div style="margin-top:32px">
                            <p class="box_topic_title">{{movieDetail.status}}</p>
                            <p class="box_topic">Status</p>
                        </div>
                        <div style="margin-top:32px">
                            <p class="box_topic_title">{{movieDetail.runtime}} minutes</p>
                            <p class="box_topic">Runtime</p>
                        </div>
                        <div style="margin-top:32px">
                            <p v-if="movieDetail.popularity" class="box_topic_title">{{math(movieDetail.popularity)}}</p>
                            <p v-if="movieDetail.popularity == 0" class="box_topic_title">0</p>
                            <p class="box_topic">Number of people in a day </p>
                        </div>
                        <div style="margin-top:32px">
                            <p v-if="movieDetail.budget" class="box_topic_title">${{math(movieDetail.budget)}}</p>
                            <p v-if="movieDetail.budget == 0" class="box_topic_title">$0</p>
                            <p class="box_topic">Budget</p>
                        </div>
                        <div style="margin-top:32px">
                            <p v-if="movieDetail.revenue" class="box_topic_title">${{math(movieDetail.revenue)}}</p>
                            <p v-if="movieDetail.revenue == 0" class="box_topic_title">$0</p>
                            <p class="box_topic">Revenue</p>
                        </div>
                        <div style="margin-top:32px">
                            <p class="box_topic_title">Keywords</p>
                            <a-row>
                                <a-col :xs="4" :sm="4" :md="4" :lg="4" :xl="4" :xxl="4" class="keyword_box" v-for="k in keyword" :key="k.id">
                                    <p class="keyword_text">{{k.name}}</p>
                                </a-col>
                            </a-row>
                        </div>
                    </div>
                </div>

            </a-col>
        </a-row>
    </div>
</div>
</template>

<script>
import axios from 'axios'
import moment from 'moment'
import search from '@/components/search'
import director from '@/components/director'
import comment from '@/components/comment'
export default {
    layout: 'main',
    components: {
        search,
        director,
        comment
    },
    data() {
        return {
            movie_id: this.$route.params.detail,
            movieDetail: {},
            videoKey: '',
            language: [],
            keyword: {},
            director: [],
            cast: [],
            recommendations: [],
            box: {}
        }
    },
    methods: {
        async getData() {
            await axios
                .get(`https://api.themoviedb.org/3/movie/${this.movie_id}?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)

                .then(response => {
                    this.movieDetail = response.data
                    // console.log('movieData = ', this.movieDetail)
                    // console.log('>>>', this.language, this.movieDetail.original_language)
                    this.movieDetail.language_name = this.language.filter(el => el.iso_639_1 === this.movieDetail.original_language).pop().english_name
                    // console.log('movieDetail : ', this.movieDetail)
                })
                .catch(err => {
                    console.log(err)
                })
            await axios
                .get(`https://api.themoviedb.org/3/movie/${this.movie_id}/videos?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)

                .then(response => {
                    this.videoKey = response.data.results[0].key
                    // console.log('videoKey : ', this.videoKey)
                })
                .catch(err => {
                    console.log(err)
                })

            await axios
                .get(`https://api.themoviedb.org/3/movie/${this.movie_id}/keywords?api_key=38c75e40ea604b41a0a54c8b05a806fc`)

                .then(response => {
                    this.keyword = response.data.keywords
                    // console.log('keyword : ', this.keyword)
                })
                .catch(err => {
                    console.log(err)
                })
            await axios
                .get(`https://api.themoviedb.org/3/movie/${this.movie_id}/credits?api_key=38c75e40ea604b41a0a54c8b05a806fc`)

                .then(response => {
                    this.director = response.data.crew
                    this.cast = response.data.cast
                    // console.log('director : ', this.director)
                    // console.log('cast : ', this.cast)
                })
                .catch(err => {
                    console.log(err)
                })
            await axios
                .get(`https://api.themoviedb.org/3/movie/${this.movie_id}/recommendations?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)

                .then(response => {
                    // this.recommendation = response.data
                    // this.recommendation = response.data
                    this.box = response.data.results
                    var i
                    if (this.box.length > 5) {
                        for (i = 0; i < 5; i++) {

                            this.recommendations.push(this.box[i])
                        }
                        // console.log('recommendations : ', this.recommendations)
                    } else {
                        for (i = 0; i < this.box.length; i++) {

                            this.recommendations.push(this.box[i])
                        }
                        // console.log('recommendations : ', this.recommendations)
                    }

                })
                .catch(err => {
                    console.log(err)
                })
        },
        async getLang() {
            await axios
                .get(`https://api.themoviedb.org/3/configuration/languages?api_key=38c75e40ea604b41a0a54c8b05a806fc`)
                .then(response => {
                    this.language = response.data
                    // console.log('language2 : ', this.language)
                })
                .catch(err => {
                    console.log(err)
                })
        },
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
        },
        math(num) {
            // console.log(num)
            var number = num.toString().replace(/\B(?<!\.\d*)(?=(\d{3})+(?!\d))/g, ",");
            return number
        }
    },
    async mounted() {
        await this.getLang()
        await this.getData()
        // await this.getVideo()

    }
}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.overview_box {
    width: 100%;
    height: 600px;
    position: relative;
}

.overview_box_backdrop {
    object-fit: cover;
    object-position: top;
    width: 100%;
    height: 600px;
    filter: brightness(0.5);
}

.overview_box_detail {
    position: absolute;
    top: 40px;
    bottom: 40px;
    left: 80px;
    right: 80px;
    width: 1120px;
    height: 520px;
    margin: auto;
}

.overview_box_poster {
    width: 373.33px;
    height: 520px;
    object-fit: cover;
    border-radius: 5px 0px 0px 5px;
}

.detail_box {
    padding: 48px 80px;
}

.movie_detail_box {
    width: 1120px;
    margin: auto;
}

.title {
    font-style: normal;
    font-weight: 800;
    font-size: 44px;
    line-height: 53px;
    display: flex;
    align-items: center;
    letter-spacing: 0.08em;
    text-transform: uppercase;

    color: #FFFFFF;

}

.release_box {
    display: flex;
    margin-top: 6px;
    width: 100%;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.release_genres {
    display: flex;

}

.release_date_box {
    width: 184px;
    height: 32px;
    background: #FADB14;
}

.release_date_text {
    font-style: normal;
    font-weight: 500;
    font-size: 24px;
    line-height: 29px;
    text-align: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #000000;

    text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.category_text {
    font-style: normal;
    font-weight: 500;
    font-size: 24px;
    line-height: 29px;
    letter-spacing: 0.08em;
    text-transform: uppercase;

    color: #FFFFFF;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.rated_box {
    margin-top: 32px;
    width: 456px;
    height: 88px;
}

.rectangle {
    width: 200px;
    height: 48px;
    border-radius: 52px;
    background-color: #262626;
    position: relative;
}

.starIcon {
    position: absolute;
    top: 4px;
    bottom: 4px;
    left: 24px;
    right: 24px;
    font-size: 24px;
}

.circle {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background-color: #262626;
    position: relative;
    cursor: pointer;
}

.icon {
    font-size: 24px;
    color: #FADB14;
    position: absolute;
    top: 12px;
    bottom: 12px;
    left: 12px;
    right: 12px;
}

.movie_detail_text_box {
    width: 752px;
    height: auto;
}

.movie_detail_text {
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    /* or 150% */

    display: flex;
    align-items: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FFFFFF;
}

.box_detail {
    width: 304px;
    height: 1450px;
    background: rgba(0, 0, 0, 0.5);
    border-radius: 5px;
    margin-left: 16px;
    padding: 32px;
}

.box_topic_title {
    font-style: normal;
    font-weight: 500;
    font-size: 24px;
    line-height: 24px;
    /* or 100% */
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FFFFFF;
}

.box_topic {
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    /* or 150% */

    display: flex;
    align-items: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FFFFFF;
}

.keyword_box {
    margin: 6px 10px 6px 0px;
    padding: 5px;
    width: auto;
    height: 24px;
    background: rgba(250, 219, 20, 0.25)
}

.keyword_text {
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 12px;
    /* identical to box height, or 150% */

    text-align: center;
    letter-spacing: 0.04em;
    text-transform: lowercase;

    color: #FFFFFF;
}

.director {
    margin-top: 32px;
    display: flex;
    overflow-x: scroll;
    overflow-y: hidden;
    white-space: nowrap;
}

.director_profile {
    width: 160px;
    height: 160px;
    object-fit: cover;
    border-radius: 5px;
}

.director_name {
    width: 160px;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 24px;
    /* identical to box height, or 150% */
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FFFFFF;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.director_job {
    width: 160px;
    font-style: normal;
    font-weight: 500;
    font-size: 16px;
    line-height: 24px;
    /* identical to box height, or 150% */

    display: flex;
    align-items: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FFFFFF;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
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

.cast {
    margin-top: 32px;
    display: flex;
    overflow-x: scroll;
    overflow-y: hidden;
    white-space: nowrap;
}

.cast_topic {
    margin-top: 32px;
    font-style: normal;
    font-weight: 800;
    font-size: 32px;
    line-height: 38px;
    display: flex;
    align-items: center;
    letter-spacing: 0.08em;
    text-transform: uppercase;

    color: #FFFFFF;
}

.cast_profile {
    width: 160px;
    height: 240px;
    object-fit: cover;
    border-radius: 5px 5px 0px 0px;
}

.cast_name_box {
    width: 160px;
    height: 48px;
    padding: 12px 8px;
    background: #FADB14;
    border-radius: 0px 0px 5px 5px;
}

.cast_name {
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 24px;
    /* identical to box height, or 150% */

    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #262626;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.rec {
    margin-top: 32px;
    display: flex;
    overflow-x: scroll;
    overflow-y: hidden;
    white-space: nowrap;
}

.rec_topic {
    margin-top: 32px;
    font-style: normal;
    font-weight: 800;
    font-size: 32px;
    line-height: 38px;
    display: flex;
    align-items: center;
    letter-spacing: 0.08em;
    text-transform: uppercase;

    color: #FFFFFF;
}

.rec_img {
    width: 288px;
    height: 160px;
    border-radius: 5px;
    object-fit: cover;
    object-position: top;
}

.rec_text {
    width: 200px;
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 24px;
    /* identical to box height, or 150% */

    display: flex;
    align-items: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FFFFFF;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

.rec_text2 {
    font-style: normal;
    font-weight: bold;
    font-size: 16px;
    line-height: 24px;
    /* identical to box height, or 150% */

    display: flex;
    align-items: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;

    color: #FFFFFF;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

#a1_2 {
    display: none
}

/* left: 54px; */
@media screen and (max-width: 1200px) {
    .detail_box {
        padding: 48px 60px;
    }

    .overview_box_detail {
        width: 90%;
        left: 60px;
    }

    .overview_box_poster {
        width: 100%;

    }

    iframe {
        width: 100%;
    }

    .movie_detail_box {
        width: 100%;
    }

    .box_detail {
        width: 100%;
    }
}

@media screen and (max-width: 1024px) {
    .movie_detail_text_box {
        width: 100%;
    }

    .keyword_text {
        font-size: 14px;
    }
}

@media screen and (max-width: 768px) {
    .detail_box {
        padding: 48px 40px;
    }

    .overview_box {
        height: 420px;
    }

    .overview_box_backdrop {
        height: 420px;
    }

    .overview_box_detail {
        left: 40px;
        height: 320px;
    }

    .overview_box_poster {
        height: 320px;
    }

    iframe {
        height: 320px;
    }

    .box_topic_title {
        font-size: 20px;
    }

    .box_topic {
        font-size: 14px;
        line-height: 16px;
    }

    .box_detail {
        padding: 32px 16px;
    }

    .keyword_text {
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }

}

@media screen and (max-width: 767px) {
    .detail_box {
        padding: 48px 20px;
    }

    .overview_box,
    .overview_box_backdrop {
        height: 848px;
    }

    .overview_box_detail {
        height: auto;
        width: 100%;
        top: 32px;
        left: 0;
        margin: auto;
    }

    .overview_box_poster {
        border-radius: 5px 5px 0 0;
    }

    .overview_box_poster,
    iframe {
        width: 324px;
        height: 424px;
        display: block;
        margin: auto;
    }

    iframe {
        height: 284px;
    }

    .release_date_box {
        padding: 0 4px;
    }

    .rated_box {
        width: 100%;
    }

    .rectangle {
        width: 90%;
        margin: auto;
    }

    .starIcon {
        font-size: 18px;
        top: 8px;
        bottom: 4px;
        left: 20px;
        right: 0;
    }

    .release_box {
        display: block;
    }

    .release_box div {
        margin-left: 0px !important;
        margin-right: 16px;
    }

    .release_genres {
        margin-top: 8px;
    }

    .box_detail {
        height: auto;
        margin: 0;

    }

    .row {
        display: flex;
        flex-flow: column;
    }

    #a2 {
        margin-top: 24px;
        width: 100%;
        order: 1;
    }

    #a1 {
        display: none;
    }

    #a1_2 {
        width: 100%;
        display: block;
        order: 2;
    }

}

@media screen and (max-width: 400px) {

    .overview_box,
    .overview_box_backdrop {
        height: 776px;
    }

    .overview_box_poster {
        width: 296px;
        height: 424px;
    }

    iframe {
        width: 296px;
        height: 208px;
    }

    .starIcon {
        left: 8px;
        top: 4px;
    }

    .ant-progress {
        width: 62px;
        height: 62px;
    }

    .rectangle {
        height: 38px;
    }

    .circle {
        width: 38px;
        height: 38px;
    }

    .icon {
        font-size: 16px;
        left: 11px;
    }

}

@media screen and (max-width: 320px) {
    .starIcon {
        top: 7px;
        left: 12px;
        font-size: 14px;
    }

    .overview_box_poster {
        width: 296px;
        height: 400px;
    }

    iframe {
        width: 296px;
    }
}
</style><style>
@media screen and (max-width: 400px) {
    .nowshowing-progress .ant-progress-inner {
        width: 54px !important;
        height: 54px !important;
    }
}
</style>
