---
title: 我的歌单
donate: true
---
<h3 class="neteat-fonts">网易云音乐</h3>
{% meting
 "156019419" 
 "netease" 
 "playlist"
 "mutex:false" 
 "listmaxheight:340px" 
 "preload:none" 
 "theme:#f40"
 "volume:0.4"
%}

<h3 class="tencent-fonts">QQ音乐</h3>
{% meting
 "1983682154" 
 "tencent" 
 "playlist"
 "mutex:false" 
 "listmaxheight:340px" 
 "preload:none" 
 "theme:#f40"
 "volume:0.4"
%}

<style>
.neteat-fonts {
    -webkit-mask-image: linear-gradient(to right, #C20C0C, red);
    background-image: linear-gradient(to right, #C20C0C, red, #C20C0C, red, #C20C0C, red, #C20C0C, red);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-size: 200% 100%;
    animation: bgp 5s infinite linear;
}

.tencent-fonts {
    -webkit-mask-image: linear-gradient(to right, #31c27c, yellow);
    background-image: linear-gradient(to right, #31c27c, yellow, #31c27c, yellow, #31c27c, yellow, #31c27c, yellow);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-size: 200% 100%;
    animation: bgp 5s infinite linear;
}


@keyframes bgp {
    0% {
        background-position: 0 0;
    }
    100% {
        background-position: -100% 0;
    }
}
</style>