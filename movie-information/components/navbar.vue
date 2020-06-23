<template>
<div>
    <div class="navbar" :class="{ 'scrolled': !view.atTopOfPage }">
        <div class="nav_mobile">
            <a href="/" class="mobile_logo"></a>
            <div class="container" @click="toggle_bar()">
                <div class="bar1"></div>
                <div class="bar2"></div>
                <div class="bar3"></div>
            </div>
        </div>

        <ul>
            <a href="/">
                <li class="menu">home</li>
            </a>
            <a href="/page/movielist?page=1" @click="movie()">
                <li class="menu">movies</li>
            </a>
            <a href="/" class="logo">
                <li style="width: 186px;height: 96px;"></li>
            </a>
            <a href="#" class="menu_cat">
                <li>category</li>
                <div class="category">
                    {{cat.id}}
                    <div class="category_box">
                        <div v-for="c in cat" :key="c.id">
                            <a :href="`/page/searchbygenres/${c.id}?page=1`">
                                <p class="category_text">{{c.name}}</p>
                            </a>
                        </div>
                    </div>
                    <div class="category_box">
                        <div v-for="c2 in cat2" :key="c2.id">
                            <a :href="`/page/searchbygenres/${c2.id}?page=1`">
                                <p class="category_text">{{c2.name}}</p>
                            </a>
                        </div>
                    </div>
                    <div class="category_box">
                        <div v-for="c3 in cat3" :key="c3.id">
                            <a :href="`/page/searchbygenres/${c3.id}?page=1`">
                                <p class="category_text">{{c3.name}}</p>
                            </a>
                        </div>
                    </div>
                    <div class="category_box">
                        <div v-for="c4 in cat4" :key="c4.id">
                            <a :href="`/page/searchbygenres/${c4.id}?page=1`">
                                <p class="category_text">{{c4.name}}</p>
                            </a>
                        </div>
                    </div>
                    <div class="category_box">
                        <div v-for="c5 in cat5" :key="c5.id">
                            <a :href="`/page/searchbygenres/${c5.id}?page=1`">
                                <p class="category_text">{{c5.name}}</p>
                            </a>
                        </div>
                    </div>
                </div>
            </a>
            <a href="#footbar">
                <li class="menu">contact</li>
            </a>
        </ul>
        <ul class="ul_mobile" v-show="toggle">
            <a href="/">
                <li class="menu">home</li>
            </a>
            <a href="/page/movielist?page=1">
                <li class="menu">movies</li>
            </a>
            <a href="/" class="logo">
                <li style="width: 186px;height: 96px;"></li>
            </a>
            <a class="menu_cat" @click="show_cat()">
                <li>category</li>
                <div class="category" v-show="showCat">
                    {{cat.id}}
                    <div class="category_box">
                        <div v-for="c in cat" :key="c.id">
                            <a :href="`/page/searchbygenres/${c.id}?page=1`">
                                <p class="category_text">{{c.name}}</p>
                            </a>
                        </div>
                    </div>
                    <div class="category_box">
                        <div v-for="c2 in cat2" :key="c2.id">
                            <a :href="`/page/searchbygenres/${c2.id}?page=1`">
                                <p class="category_text">{{c2.name}}</p>
                            </a>
                        </div>
                    </div>
                    <div class="category_box">
                        <div v-for="c3 in cat3" :key="c3.id">
                            <a :href="`/page/searchbygenres/${c3.id}?page=1`">
                                <p class="category_text">{{c3.name}}</p>
                            </a>
                        </div>
                    </div>
                    <div class="category_box">
                        <div v-for="c4 in cat4" :key="c4.id">
                            <a :href="`/page/searchbygenres/${c4.id}?page=1`">
                                <p class="category_text">{{c4.name}}</p>
                            </a>
                        </div>
                    </div>
                    <div class="category_box">
                        <div v-for="c5 in cat5" :key="c5.id">
                            <a :href="`/page/searchbygenres/${c5.id}?page=1`">
                                <p class="category_text">{{c5.name}}</p>
                            </a>
                        </div>
                    </div>
                </div>
            </a>
            <a href="#footbar">
                <li class="menu">contact</li>
            </a>
        </ul>

    </div>

</div>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            view: {
                atTopOfPage: true
            },
            gen: {},
            cat: [],
            cat2: [],
            cat3: [],
            cat4: [],
            cat5: [],
            toggle: false,
            showCat: false
        }
    },
    beforeMount() {
        window.addEventListener('scroll', this.handleScroll);
    },
    methods: {
        // show() {
        //     this.Isshow = !this.Isshow
        // },
        // movie(){
        //     this.$router.push('movielist/'+)
        // }
        getgenres() {
            axios
                .get(`https://api.themoviedb.org/3/genre/movie/list?api_key=38c75e40ea604b41a0a54c8b05a806fc&language=en-US`)

                .then(response => {
                    this.gen = response.data.genres
                    // console.log('gen : ', this.gen)
                    var i, j, k, l, m

                    for (i = 0; i < 4; i++) {
                        this.cat.push(this.gen[i])
                    }
                    // console.log("cat : ", this.cat)
                    for (j = 4; j < 8; j++) {
                        this.cat2.push(this.gen[j])
                    }
                    // console.log("cat2 : ", this.cat2)
                    for (k = 8; k < 12; k++) {
                        this.cat3.push(this.gen[k])
                    }
                    // console.log("cat3 : ", this.cat3)
                    for (l = 12; l < 16; l++) {
                        this.cat4.push(this.gen[l])
                    }
                    // console.log("cat4 : ", this.cat4)
                    for (m = 16; m < 19; m++) {
                        this.cat5.push(this.gen[m])
                    }
                    // console.log("cat5 : ", this.cat5)
                    // console.log(this.gen.genres[5])
                })
                .catch(err => {
                    console.log(err)
                })
        },
        handleScroll() {
            // when the user scrolls, check the pageYOffset
            if (window.pageYOffset > 0) {
                // user is scrolled
                if (this.view.atTopOfPage) this.view.atTopOfPage = false
            } else {
                // user is at top of page
                if (!this.view.atTopOfPage) this.view.atTopOfPage = true
            }
        },
        toggle_bar() {
            this.toggle = !this.toggle
            this.showCat = false
        },
        show_cat() {
            this.showCat = !this.showCat
        }
    },
    mounted() {
        this.getgenres()
       
    }
}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    color: white;
}

.navbar {
    display: flex;
    justify-content: center;
    width: 100%;
    height: 96px;
    /* border: 1px solid white; */
    position: fixed;
    top: 0;
    background-color: #FADB14;
    z-index: 3;
    transition: 0.3s;
}

.navbar.scrolled {
    background: #262626;
}

.navbar.scrolled li {
    color: #FADB14;
}

.nav_mobile {
    display: flex;
    justify-content: space-between;
}

ul {
    display: flex;
    justify-content: space-between;
    list-style: none;
}

li {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 128px;
    height: 96px;
    font-style: normal;
    font-weight: bold;
    font-size: 20px;
    line-height: 24px;
    text-align: center;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: #000000;
    cursor: pointer;
}

.menu,
.menu_cat {
    transition: 0.2s;
}

.menu:hover {
    background: #262626;
    color: #FADB14;
}

.menu_cat:hover{
    background: #262626;
    color: #FADB14;
}

.menu_cat:hover li {
    background: #262626;
    color: #FADB14;
}

.logo {
    width: 186px;
    height: 96px;
    background: url('~@/assets/img/logo.png');
    transition: 0.3;
}

.navbar.scrolled .logo {
    background: url('~@/assets/img/logo_scrolled.png');
}

.navbar.scrolled .menu:hover {
    background: #FADB14;
    color: rgb(43, 43, 43);
}

.navbar.scrolled .menu_cat:hover {
    background: #FADB14;
    color: rgb(43, 43, 43);
}

.category {
    width: 100%;
    height: 200px;
    display: none;
    justify-content: center;
    background: #262626;
    position: fixed;
    top: 96px;
    left: 0px;
    padding: 20px 0px;
    z-index: 3;
    transition: 0.3s;
}

/* .category:hover {
    display: flex;
} */

/* .category:hover .menu_cat{
    background: #262626;
    color: #FADB14;
} */

.menu_cat:hover .category {
    display: flex;
}

.category_box {
    width: 200px;
    height: 160px;
    border-left: 1px solid #FADB14;
    padding: 20px 24px;
    display: block;
}

.category_text {
    margin-bottom: 8px;
    font-style: normal;
    font-weight: bold;
    font-size: 20px;
    line-height: 24px;
    /* identical to box height */
    letter-spacing: 0.08em;
    text-transform: uppercase;

    color: #FADB14;
    transition: 0.3;
}

.category_text:hover {
    color: #bba410;
}

.mobile_logo {
    width: 52px;
    height: 32px;
    display: none;
    background: url('~@/assets/img/logo_mobile.png');
}

.navbar.scrolled .mobile_logo {
    width: 52px;
    height: 32px;
    display: none;
    background: url('~@/assets/img/logo_mobile_scrolled.png');
}

.ul_mobile {
    display: none;
}

.container {
    display: none;

}

.bar1,
.bar2,
.bar3 {
    width: 22px;
    height: 4px;
    background-color: #333;
    margin: 4px 0;
    border-radius: 5px;
    transition: 0.4s;
}

.navbar.scrolled .bar1,
.navbar.scrolled .bar2,
.navbar.scrolled .bar3 {
    background-color: #FADB14;
}

@media screen and (max-width: 767px) {
    .navbar {
        display: block;
        height: 56px;
    }

    .mobile_logo,
    .navbar.scrolled .mobile_logo {
        display: block;
        margin: 12px 16px;
    }

    ul {
        display: none;

    }

    .ul_mobile {
        display: block;
        background: #FADB14;
        transition: 0.3s;
    }

    .navbar.scrolled .ul_mobile {
        background: #262626;
    }

    a .logo,
    .logo li {
        display: none;
    }

    li {
        margin: auto;
        width: 100%;
        height: 50px;
        border-bottom: 1px groove #262626;
    }

    .navbar.scrolled li{
        border-bottom: 0.1px groove #FADB14;
    }

    .container {
        display: inline-block;
        cursor: pointer;
        padding: 14px;
    }

    .category {
        top: 206px;
        width: 100%;
        overflow-x: scroll;
        overflow-y: hidden;
        white-space: nowrap;
        justify-content: flex-start;
        padding-left: 8px;
    }

}
</style>
