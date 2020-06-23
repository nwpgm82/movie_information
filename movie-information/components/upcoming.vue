<template>
<div>
    <a-carousel autoplay>
        <div v-for="i in box" :key="i.id" style="position:relative;top:8px;">
            <img :src="`https://image.tmdb.org/t/p/original${i.backdrop_path}`" alt="" class="upcoming_backdrop">
            <a-row class="row">
                <a-col :sm="24" :md="8" :lg="8" :xl="8" :xxl="8">
                    <img :src="`https://image.tmdb.org/t/p/original${i.poster_path}`" alt="" class="upcomimg_poster">
                    <div class="upcoming_date">
                        <p>{{formatDate(i.release_date)}}</p>
                    </div>
                </a-col>
                <a-col :sm="24" :md="16" :lg="16" :xl="16" :xxl="16">
                    <div class="upcoming_movie_bg">
                        <div class="upcoming_movie_topic">
                            <p>{{i.title}}</p>
                        </div>
                        <div class="upcoming_movie_text">
                            {{i.overview}}
                        </div>
                        <div class="btn_menu">
                            <div class="btn">
                                <button @click="showModal(i.id)">trailer video</button>
                                <a-modal v-model="visible" @ok="handleOk()" destroyOnClose>
                                    <iframe width="1280" height="720" :src="`https://www.youtube.com/embed/${movie_key}`" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
                                </a-modal>
                            </div>

                            <a :href="`https://www.youtube.com/watch?v=${movie_key}`" class="btn_mobile" @click="get_video_mobile(i.id)"><button>trailer video</button></a>
                            <a :href="`/page/detail/${i.id}`">See more detail</a>
                        </div>
                    </div>
                </a-col>
            </a-row>
        </div>
    </a-carousel>
</div>
</template>

<script>
import axios from 'axios';
import moment from 'moment'
export default {
    data() {
        return {
            upcoming: {},
            box: [],
            videoDetail: {},
            key: '',
            visible: false,
            movie_key: ''
        }
    },
    methods: {
        formatDate(date) {
            return moment(date).format('DD MMMM YYYY')
        },
        async showModal(i) {
            this.visible = true;
            const movie_key = await this.$axios.$get(`https://api.themoviedb.org/3/movie/${i}/videos?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)
            this.movie_key = movie_key.results[0].key
            // axios
            //     .get(`https://api.themoviedb.org/3/movie/${i}/videos?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)
            //     .then(response => {
            //         return this.num = response.data.results[0].key
            //         // this.videoDetail = response.data.results[0].key
            //         // console.log('Current page : ', this.current)
            //     })
            //     .catch(err => {
            //         console.log(err)
            //     })
        },
        handleOk(e) {
            // console.log(e);
            this.visible = false;
        },
        async get_video_mobile(j) {
            const movie_key = await this.$axios.$get(`https://api.themoviedb.org/3/movie/${j}/videos?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)
            this.movie_key = movie_key.results[0].key
        }
    },
    async mounted() {
        await axios
            .get(`https://api.themoviedb.org/3/movie/upcoming?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)

            .then(response => {
                this.upcoming = response.data
                var i
                for (i = 0; i < 5; i++) {
                    this.box.push(this.upcoming.results[i])
                }
                // console.log(this.box)
            })
            .catch(err => {
                console.log(err)
            })
        // await axios
        //     .get(`https://api.themoviedb.org/3/movie/${this.box.id}/videos?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)
        //     .then(response => {
        //         this.videoDetail = response.data
        //         console.log('Current page : ', this.current)
        //     })
        //     .catch(err => {
        //         console.log(err)
        //     })
        // this.key = await this.videoDetail.results[0].key
    },
}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.upcoming_backdrop {
    object-fit: cover;
    object-position: top;
    width: 100%;
    height: 544px;
    filter: brightness(0.5);

}

.row {
    width: 976px;
    height: 496px;
    margin: auto;
    position: absolute;
    top: 24px;
    left: 152px;
    right: 152px;
    bottom: 24px;
}

.upcomimg_poster {
    width: 325.33px;
    height: 448px;
}

.upcoming_date {
    width: 325.33px;
    height: 48px;
    background-color: #FADB14;
    font-style: normal;
    font-weight: 500;
    font-size: 32px;
    line-height: 44px;
    text-align: center;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #000000;
    text-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

.upcoming_movie_bg {
    width: 648px;
    height: 496px;
    background: rgba(0, 0, 0, 0.5);
    padding: 56px 32px;
}

.upcoming_movie_topic {
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

.upcoming_movie_text {
    margin-top: 32px;
    font-style: normal;
    font-weight: normal;
    font-size: 24px;
    line-height: 32px;
    /* or 133% */
    width: 584px;
    height: 192px;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    color: #FFFFFF;
    overflow: hidden;
    white-space: pre-line;
    text-overflow: ellipsis;
}

button {
    width: 160px;
    height: 48px;
    border: 1px solid #FADB14;
    border-radius: 5px;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
    background: transparent;
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 32px;
    /* identical to box height, or 200% */

    text-align: center;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    color: #FFFFFF;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background: #FADB14;
    color: #262626;
    box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
}

a {
    margin-left: 32px;
    font-style: normal;
    font-weight: normal;
    font-size: 16px;
    line-height: 32px;
    /* identical to box height, or 200% */

    display: flex;
    align-items: center;
    letter-spacing: 0.04em;
    text-decoration-line: underline;
    text-transform: uppercase;

    color: #FFFFFF;
    cursor: pointer;
}

.btn_menu {
    margin-top: 35px;
    display: flex;
}

.btn_mobile {
    display: none;
}

@media screen and (max-width: 1199px) {
    .row {
        right: 0;
        left: 72px;
        padding: 16px;
    }

    .upcomimg_poster {
        width: 100%;
        height: 384px;
    }

    .upcoming_date {
        width: 100%;
        font-size: 28px;
    }

    .upcoming_date {
        width: 100%;
        font-size: 28px;
    }

    .upcoming_movie_bg {
        width: 100%;
        height: 432px;
        padding: 32px;
    }

    .upcoming_movie_text {
        margin-top: 8px;
        width: 100%;
    }

}

@media screen and (max-width: 1024px) {
    .row {
        right: 0;
        left: 6px;
        padding: 16px;
    }
}

@media screen and (max-width: 991px) {
    .row {
        right: 0;
        left: 0;
        width: 100%;
    }
}

@media screen and (max-width: 767px) {
    .upcoming_backdrop {
        height: 848px;
    }

    .row {
        top: 0;
        bottom: 318px;
    }

    .upcomimg_poster {
        margin: 0 auto;
        width: 324px;
        height: 384px;
        object-fit: cover;
        object-position: center;
    }

    .upcoming_date {
        width: 324px;
        height: 48px;
        margin: 0 auto;
    }

    .upcoming_movie_bg {
        width: 324px;
        height: auto;
        margin: auto;
        padding: 16px;
    }

    .upcoming_movie_topic p {
        white-space: nowrap;
        width: 292px;
        color: white;
        overflow: hidden;
        text-overflow: ellipsis;
    }

    .upcoming_movie_text {
        margin-top: 6px;
        width: 292px;
        height: 120px;
        display: -webkit-box;
        -webkit-line-clamp: 5;
        -webkit-box-orient: vertical;
        overflow: hidden;
        text-overflow: ellipsis;
        font-style: normal;
        font-weight: 500;
        font-size: 16px;
        line-height: 24px;
        /* or 150% */
        letter-spacing: 0.04em;
        text-transform: uppercase;
        white-space: normal;
        color: #FFFFFF;

        opacity: 0.6;
    }

    .btn_menu {
        display: block;
        margin-top: 16px;
    }

    button {
        width: 292px;
    }

    a {
        margin: 16px 0;
        justify-content: center;
    }

    .btn {
        display: none;
    }

    .btn_mobile {
        display: block;
    }

}

@media screen and (max-width: 400px) {

    .upcomimg_poster,
    .upcoming_movie_bg {
        width: 296px;
        height: 400px;
    }

    .upcoming_movie_bg {
        height: auto;
    }

    .upcoming_date {
        width: 296px;
    }

    .upcoming_movie_text,
    .upcoming_movie_topic,
    button {
        width: 264px;
    }
}

@media screen and (max-width: 1280px) {
    iframe {
        width: 70%;
        height: 600px;
        margin: auto;
        display: block;
    }
}

@media screen and (max-width: 320px) {
    .row {
        left: -8px;
    }
}
</style>
<style>
.ant-modal-close-x{
    color: white !important;
}
</style>
