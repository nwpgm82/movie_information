<template>
<div class="bottombar" id="footbar">
    <img src="~/assets/img/logo2.png" alt="" class="logo">
    <div class="social">
        <a href="#" class="fb_logo"></a>
        <a href="#" class="ig_logo"></a>
        <a href="#" class="tw_logo"></a>
        <a href="#" class="go_logo"></a>
    </div>
</div>
</template>

<script>
export default {

}
</script>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.bottombar {
    width: 100%;
    height: 104px;
    display: flex;
    justify-content: space-between;
    background: #FADB14;
    padding: 20px 50px;

}

.logo {
    width: 363px;
    height: 64px;
}

.social {
    display: grid;
    grid-template-columns: auto auto auto auto;
    grid-gap: 32px;
    margin: auto 0;
}

.fb_logo {
    width: 48px;
    height: 48px;
    background: url('~@/assets/img/facebook.png');
    cursor: pointer;
    transition: 0.3s;
}

.ig_logo {
    width: 48px;
    height: 48px;
    background: url('~@/assets/img/instagram.png');
    cursor: pointer;
    transition: 0.3s;
}

.tw_logo {
    width: 48px;
    height: 48px;
    background: url('~@/assets/img/twitter.png');
    cursor: pointer;
    transition: 0.3s;
}

.go_logo {
    width: 48px;
    height: 48px;
    background: url('~@/assets/img/google+.png');
    cursor: pointer;
    transition: 0.3s;
}

.fb_logo:hover {
    background: url('~@/assets/img/facebook_hover.png');
}

.ig_logo:hover {
    background: url('~@/assets/img/instagram_hover.png');
}

.tw_logo:hover {
    background: url('~@/assets/img/twitter_hover.png');
}

.go_logo:hover {
    background: url('~@/assets/img/google+_hover.png');
}

@media screen and (max-width: 767px) {
    .bottombar {
        display: block;
        height: auto;
        padding: 16px;
    }

    .logo {
        width: 80%;
        height: 80%;
        display: block;
        margin: auto;
    }

    .social {
        margin-top: 32px;
    }

    .fb_logo,
    .ig_logo,
    .tw_logo,
    .go_logo {
        width: 48px;
        height: 48px;
        display: block;
        margin: auto;
    }

}
</style>
