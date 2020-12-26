<template>
  <div class="container">
      
      <!-- Card with iframe -->
      <!-- <b-card no-body>
        <b-card-header>
          <div class="iframe-container">
            <iframe src="https://player.vimeo.com/video/118897935?title=0&byline=0&portrait=0" width="640" height="360" frameborder="0" allow="autoplay; fullscreen" allowfullscreen class="responsive-iframe"></iframe>
          </div>
        </b-card-header>
        <b-card-body>
          Hola
        </b-card-body>
      </b-card> -->
      


  </div>
</template>

<script>
export default {

}
</script>

<style>


/* iframe classes */
.iframe-container {
  position: relative;
  overflow: hidden;
  width: 100%;
  padding-top: 56.25%; /* 16:9 Aspect Ratio (divide 9 by 16 = 0.5625) */
}

/* Then style the iframe to fit in the container div with full height and width */
.responsive-iframe {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100%;
}
</style>