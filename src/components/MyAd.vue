<template>
  <div class="my-ad">
    <div class="ad-background">
      <iframe
        class="large-screen"
        src="//rcm-na.amazon-adsystem.com/e/cm?o=1&p=48&l=ur1&category=amazonvideosubs&banner=13SDN022FT730ZKSWBR2&f=ifr&linkID=650ccc4e260b0e7048db60e8bdf586eb&t=399120-20&tracking_id=399120-20"
        width="728"
        height="90"
        scrolling="no"
        border="0"
        marginwidth="0"
        style="border:none;"
        frameborder="0"
      ></iframe>
    </div>
    <iframe
      class="small-screen"
      src="//rcm-na.amazon-adsystem.com/e/cm?o=1&p=12&l=ur1&category=amazonvideosubs&banner=1NC5AMTYQY33988ZD002&f=ifr&linkID=4747bcad8d8ca0d9a445c67e229cc7a6&t=399120-20&tracking_id=399120-20"
      width="300"
      height="250"
      scrolling="no"
      border="0"
      marginwidth="0"
      style="border:none;"
      frameborder="0"
    ></iframe>
  </div>
</template>

<script>
export default {
  name: "MyAd"
};
</script>

<style>
.my-ad {
  position: relative;
  top: -5px;
  display: flex;
  justify-content: center;
}

iframe {
  margin: auto;
}
iframe.small-screen {
  display: none;
}

@media screen and (max-width: 800px) {
  iframe.large-screen {
    display: none;
  }
  iframe.small-screen {
    display: block;
  }
}
</style>
