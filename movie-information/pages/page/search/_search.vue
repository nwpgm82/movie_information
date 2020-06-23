<template>
<div style="background:rgba(38, 38, 38, 0.65);">
    <search />
    <div class="box">
        <div class="menu_list">
            <p class="topic" style="color: #FADB14;">Result search : {{this.$route.params.search}}</p>
        </div>

        <a-row class="row">
            <a-col :xs="12" :sm="12" :md="8" :lg="6" :xl="6" :xxl="6" v-for="i in search.results" :key="i.id">
                <div class="card">
                    <a :href="`/page/detail/${i.id}`">
                        <img v-if="i.poster_path" :src="`https://image.tmdb.org/t/p/original/${i.poster_path}`" :alt="i.title" class="movie_img">
                        <img v-if="i.poster_path == null" class="movie_img" src="https://upload.wikimedia.org/wikipedia/commons/f/fc/No_picture_available.png" alt="">
                        <p class="movie_topic">{{i.title}}</p>
                        <p class="movie_date">{{formatDate(i.release_date)}}</p>
                        <div class="circle_box">
                            <a-progress class="search-progress" type="circle" :percent="`${i.vote_average}`*10" :stroke-width="10" :strokeColor="setColor(i.vote_average)" :width="40" />
                        </div>
                    </a>
                </div>
            </a-col>
        </a-row>
        <div style="display:flex;justify-content:center;padding:32px 0;">
            <a-pagination v-model="current" :total="search.total_results" :page-size="20" class="pagination" @change="onChange" />
        </div>
    </div>

</div>
</template>

<script>
import search from '@/components/search'
import axios from 'axios';
import moment from 'moment'
export default {
    layout: 'main',
    components: {
        search
    },
    data() {
        return {
            current: +this.$route.query.page,
            search_params: this.$route.params.search,
            search: {}
        }
    },
    methods: {
        detail(i) {
            this.$router.push('/page/detail/' + i)
            // console.log(i)
        },
        onSearch(value) {
            // console.log(value);
            this.$router.push('/page/search/' + value)
            document.body.scrollTop = 0;
            document.documentElement.scrollTop = 0;
        },
        async onChange(current) {
            var p = await new URLSearchParams(window.location.search)
            await p.set('page', current)
            await history.replaceState(null, null, "?" + p.toString())
            await this.getData()
            document.body.scrollTop = 0;
            document.documentElement.scrollTop = 0;
            // this.current = current;
            // console.log('Change page to : ', this.current)
            // this.getData()
            // this.$router.push(`/page/search/${this.search_params}/current/${this.current}`)
            // if (this.current == 1) {
            //     this.$router.push('/')
            // }
        },
        formatDate(date) {
            return moment(date).format('DD MMMM YYYY')
        },
        getData(current=1) {
             var p = new URLSearchParams(window.location.search)
            this.current = +p.get('page')
            axios
                .get(`https://api.themoviedb.org/3/search/movie?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US&query=${this.search_params}&page=${this.current}&include_adult=false`)

                .then(response => {
                    this.search = response.data
                    // console.log('Current page : ', this.current)
                })
                .catch(err => {
                    console.log(err)
                })
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
        this.getData()
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
    margin: auto;
}

.topic_box {
    width: 1152px;
    height: 64px;
    margin: auto;
    padding: 20px 24px;
    background: #FADB14;
    border-radius: 5px 5px 0px 0px;
}

.menu_list {
    display: flex;
    justify-content: space-between;
    width: 960px;
    height: 56px;
    background: rgba(0, 0, 0, 0.5);
    border-radius: 5px;
    margin: auto;
    padding: 6px 16px;
}

.topic {
    font-style: normal;
    font-weight: bold;
    font-size: 20px;
    line-height: 29px;
    display: flex;
    align-items: center;
    letter-spacing: 0.08em;
    text-transform: uppercase;

    color: #FADB14;
}

.box {
    width: 1152px;
    height: 2088px;
    margin: auto;
    padding: 0 24px;
    /* background: #E5E5E5; */
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
    right: -4px;
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
    .menu_list {
        width: 100%;
    }

    .box {
        width: 100%;
        height: 100%;
    }

    .row {
        width: 100%;
    }

    .circle_box {
        right: -2px;
    }
}

@media screen and (max-width: 767px) {
    .box{
        padding: 0 12px;
    }
    .topic_box {
        width: 90%;
    }

    .topic{
        width: 100%;
        font-size: 16px !important;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
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

    .topic,
    .topic_dropdown {
        font-size: 14px;
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
.search-progress .ant-progress-text {
    font-size: 14px;
}

.pagination .ant-pagination-item {
    display: inline-block;
    min-width: 32px;
    height: 32px;
    margin-right: 8px;
    font-family: Arial;
    line-height: 30px;
    text-align: center;
    vertical-align: middle;
    list-style: none;
    background-color: transparent;
    border: 1px solid #FADB14;
    border-radius: 4px;
    outline: 0;
    cursor: pointer;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    /* color: #FADB14; */
}

.pagination a {
    color: #FADB14;
}

.pagination .ant-pagination-prev .ant-pagination-item-link,
.ant-pagination-next .ant-pagination-item-link {
    display: block;
    height: 100%;
    font-size: 12px;
    text-align: center;
    background-color: transparent;
    border: 1px solid #FADB14;
    border-radius: 4px;
    outline: none;
    transition: all 0.3s;
}

.pagination .ant-pagination-jump-prev .ant-pagination-item-container .ant-pagination-item-ellipsis,
.ant-pagination-jump-next .ant-pagination-item-container .ant-pagination-item-ellipsis {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    display: block;
    margin: auto;
    color: #FADB14;
    letter-spacing: 2px;
    text-align: center;
    text-indent: 0.13em;
    opacity: 1;
    transition: all 0.2s;
}

.pagination .ant-pagination-prev,
.ant-pagination-next,
.ant-pagination-jump-prev,
.ant-pagination-jump-next {
    display: inline-block;
    min-width: 32px;
    height: 32px;
    color: #FADB14;
    font-family: Arial;
    line-height: 32px;
    text-align: center;
    vertical-align: middle;
    list-style: none;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.3s;
}

.pagination .ant-pagination-item-active a {
    color: #262626;
    background-color: #FADB14;
}

.pagination .ant-pagination-item:hover a {
    color: #262626;
    background-color: #FADB14;
}

.pagination .ant-pagination-jump-prev .ant-pagination-item-container .ant-pagination-item-link-icon,
.ant-pagination-jump-next .ant-pagination-item-container .ant-pagination-item-link-icon {
    display: inline-block;
    font-size: 12px;
    font-size: 12px \9;
    transform: scale(1) rotate(0deg);
    color: #FADB14;
    letter-spacing: -1px;
    opacity: 0;
    transition: all 0.2s;
}

.pagination .ant-pagination-disabled a,
.ant-pagination-disabled:hover a,
.ant-pagination-disabled:focus a,
.ant-pagination-disabled .ant-pagination-item-link,
.ant-pagination-disabled:hover .ant-pagination-item-link,
.ant-pagination-disabled:focus .ant-pagination-item-link {
    color: #FADB14;
    border-color: #FADB14;
    background-color: transparent;
    cursor: not-allowed;
}

.pagination .ant-pagination-next:hover .ant-pagination-item-link,
.ant-pagination-prev:hover .ant-pagination-item-link {
    color: #262626;
    border-color: #FADB14;
    background-color: #FADB14;
}

@media screen and (max-width: 399px) {
    .pagination .ant-pagination-item {
        min-width: 28px !important;
        height: 28px !important;
    }

}
</style>
