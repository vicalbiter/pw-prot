<template>
  <div class="video-card">
    <div class="video-card-header">
        <img src="https://picsum.photos/id/1018/320/180" alt="" class="video-card-img">
        <div class="header-pills">
            <div class="event-pill"> ¡Nuevo! </div>
        </div>
        <div class="play-button-wrapper">
            <i class="fa fa-play play-button"></i>
        </div>
    </div>
    <div class="video-card-content">
        <div class="top-info">
            <div>Tipo</div>
            <div>Fecha</div>
        </div>
        <div class="center-info">
            <h3>Título del Video</h3>
        </div>
        <div class="bottom-info">
            <div class="bottom-info-item">Dificultad</div>
            <div class="bottom-info-item">Duración</div>
        </div>
        <div class="bottom-info-bells"><i class="fa fa-rocket"></i></div>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style>

.video-card {
    /* max-width: 320px; */
    width: 100%;
    height: auto;
    /* border: solid 1px rgb(173, 173, 173); */
    border-radius: 10px;
    /* box-shadow: 3px 3px rgba(0,0,0,0.2); */
    transition: 0.5s;
    margin: 10px;
}

.video-card:hover {
    box-shadow: 10px 10px 10px rgba(0,0,0,0.2);
    transform: scale(1.05);
}

.video-card-header {
    position: relative;
    /* max-height: 180px; */
    cursor: pointer;
    padding: 0;
    margin: 0;
}

.video-card-header::after {
    content: "";
    display: block;
    width: 100%;
    height: 100%;
    background-color: #333;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
    position: absolute;
    top: 0;
    left: 0;
    opacity: 0.3;
    z-index: 0;
}

.video-card-header > * {
    z-index: 10;
}

.video-card-img {
    width: 100%;
    height: auto;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}

.header-pills {
    position: absolute;
    display: flex;
    width: 100%;
    top: 5%;
    left: -3%;
    color: red;
}

.event-pill {
    /* border: solid 1px #333; */
    /* border-radius: 1rem; */
    background-color: red;
    color: white;
    font-size: 0.7rem;
    font-weight: bold;
    padding: 0.5rem;
    letter-spacing: 1px;
}

.play-button-wrapper {
    position: absolute;
    width: 100%;
    display: flex;
    justify-content: center;
    font-size: 1.2rem;
    bottom: 35%;
}

.play-button {
    padding: 0.8rem 1rem;
    color: white;
    border-radius: 50%;
    background-color: red;
    cursor: pointer;
    box-shadow: 0 2px 4px rgba(0,0,0,0.5);
}

.play-button:hover {
    background-color: rgb(255, 64, 64);
}

.video-card-content {
    position: relative;
    padding: 1rem 1rem 1.5rem 1rem;
}

.top-info {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    font-size: 1rem;
}

.center-info {
    margin: 0.5rem 0 0 0;
    letter-spacing: 1px;
    font-weight: bold;
}

.center-info h3 {
    margin: 0;
}

.bottom-info {
    display: flex;
    flex-direction: row;
    margin: 0.7rem 0 0 0;
    font-size: 0.9rem;
    justify-content: start;
    align-items: center;
}

.pill {
    margin: 0 1rem 1rem 0;
    /* border: solid 1px #333; */
    padding: 0.5rem;
    border-radius: 1rem;
    box-shadow: 0.5px 0.5px #333;
    background-color: rgba(0, 0, 0, 0.3);
    color: #fff;
    /* font-size: 0.8rem; */
}

/* Bottom Alternative */
.bottom-info-item {
    margin-right: 1rem;
}

.bottom-info-bells {
    position: absolute;
    font-size: 1rem;
    padding: 0.3rem 0.5rem;
    border: solid 1px black;
    border-radius: 50%;
    right: 1rem;
    bottom: 1rem;
}
</style>