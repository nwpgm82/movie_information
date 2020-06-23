<template id="top">
<div>
    <navbar />
    <totop/>
    <div class="content_main">
        <nuxt />
    </div>
    <bottombar/>
</div>
</template>

<script>
import navbar from '@/components/navbar'
import bottombar from '@/components/bottombar'
import totop from '@/components/clicktotop'
export default {
    components: {
        navbar,
        bottombar,
        totop
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Barlow+Condensed:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Barlow:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

* {
    font-family: 'Barlow Condensed', sans-serif;
}

html,
body {
    width: 100%;
    background: url("https://www.pixelstalk.net/wp-content/uploads/2016/09/Video-Wallpapers.jpg");
    min-height: 500px;
    /* Create the parallax scrolling effect */
    background-attachment: fixed;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    scroll-behavior: smooth;
}

.content_main{
    margin-top:96px;
}

.ant-input {
    font-family: 'Barlow', sans-serif;
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-variant: tabular-nums;
    list-style: none;
    font-feature-settings: 'tnum', "tnum";
    position: relative;
    display: inline-block;
    width: 536px;
    height: 48px;
    padding: 4px 11px;
    color: white;
    font-size: 14px;
    line-height: 1.5;
    background: #434343;
    border-radius: 2px;
    background-image: none;
    border: none;
    transition: all 0.3s;
}

.ant-btn-primary {
    color: black;
    background-color: #FADB14;
    border-color: #FADB14;
    ;
    height: 48px;
    text-shadow: 0 -1px 0 rgba(0, 0, 0, 0.12);
    box-shadow: 0 2px 0 rgba(0, 0, 0, 0.045);
}

.ant-btn-primary:hover {
    background: #d6bc13;
    border-color: #d6bc13;
}

i.anticon.anticon-search {
    color: black;
}

.ant-modal {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    color: rgba(0, 0, 0, 0.65);
    font-size: 14px;
    font-variant: tabular-nums;
    line-height: 1.5;
    list-style: none;
    font-feature-settings: 'tnum', "tnum";
    position: relative;
    top: 100px;
    width: auto;
    margin: 0 auto;
    padding-bottom: 24px;
    pointer-events: none;
    width: 1280px !important;
    height: 720px !important;
}

.ant-modal-mask {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 1000;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.15);
    filter: alpha(opacity=50);
}

.ant-modal-content {
    width: auto;
    position: relative;
    background-color: transparent;
    background-clip: padding-box;
    border: 0;
    border-radius: 4px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0);
    pointer-events: auto;
}

.ant-modal-body {
    padding: 60px 0px 0px 0px;
    font-size: 14px;
    line-height: 1.5;
    word-wrap: break-word;
    width: 100%;
}

.ant-modal-close {
    position: absolute;
    top: 0;
    right: -48px;
    z-index: 10;
    padding: 0;
    color: rgba(0, 0, 0, 0.45);
    font-weight: 700;
    line-height: 1;
    text-decoration: none;
    background: transparent;
    border: 0;
    outline: 0;
    cursor: pointer;
    transition: color 0.3s;
}

.ant-modal-footer {
    display: none;
}

/* .anticon {
    display: inline-block;
    color: white;
    font-style: normal;
    line-height: 0;
    text-align: center;
    text-transform: none;
    vertical-align: -0.125em;
    text-rendering: optimizeLegibility;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
} */

.ant-progress {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    color: rgba(0, 0, 0, 0.65);
    font-size: 14px;
    font-variant: tabular-nums;
    line-height: 1.5;
    list-style: none;
    font-feature-settings: 'tnum', "tnum";
    display: inline-block;
    background: azure;
    width: 72px;
    height: 72px;
    border-radius: 50%;
    position: relative;
    background-color: #262626;
}

.ant-progress-circle .ant-progress-text {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 100%;
    margin: 0;
    padding: 0;
    color: rgba(0, 0, 0, 0.65);
    line-height: 1;
    white-space: normal;
    text-align: center;
    transform: translate(-50%, -50%);
    font-weight: bold;
    font-size: 20px;
    /* identical to box height */
    color: #FFFFFF;
}

.ant-progress-circle .ant-progress-inner {
    position: relative;
    line-height: 1;
    background-color: #262626;
    top: 4px;
    left: 4px;
}

.ant-progress-circle-trail {
    stroke: #3B3B3B !important;
}

@media screen and (max-width: 767px){
    .content_main{
        margin-top: 56px;
    }
}
</style>
