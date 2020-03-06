<template>
  <div id="Video">
    <h2>{{this.video.title}}</h2>
    <video
      id="video"
      controls
      width="700"
      height="450"
      v-on:ended="onEnd()"
      v-on:canplay="emitLoaded()"
    >
      <source type="video/mp4" />
    </video>
    <br />
    <span id="view_count">
      <strong>{{this.video.views}} views</strong>
    </span>
    <li>
      <ul>
        <button id="like" v-on:click="like()">
          <img src="../assets/thumbs_up.png" height="20" width="20" />
          {{this.video.likes}}
        </button>
        <button id="dislike" v-on:click="dislike()">
          <img src="../assets/thumbs_down.png" height="20" width="20" />
          {{this.video.dislikes}}
        </button>
      </ul>
    </li>
  </div>
</template>

<script>
export default {
  name: "Video",
  props: {
    video: Object
  },
  watch: {
    video: function() {
      document.getElementById("video").src = this.video.video;
      document.getElementById("video").load();
    }
  },
  methods: {
    onEnd() {
      this.video.views++;
    },
    like() {
      this.video.likes++;
    },
    dislike() {
      this.video.dislikes++;
    },
    emitLoaded() {
      this.video.show = false;
      this.$emit("video_loaded", this.video);
    }
  }
};
</script>

<style scoped>
video {
  margin-top: 50px;
}

li {
  display: inline-block;
  margin-left: 275px;
}

li button {
  margin-top: -10px;
  padding: 10px;
  border-color: transparent;
  font-size: 20px;
  background-color: transparent;
  color: rgb(250, 166, 26);
  text-align: center;
}

span {
  margin-top: -10px;
  padding: 10px;
  border-color: transparent;
  font-size: 20px;
  color: rgb(229, 140, 27);
  background-color: transparent;
  text-align: center;
}

#dislike:hover {
  cursor: pointer;
}

#like:hover {
  cursor: pointer;
}
div h2 {
  position: absolute;
  margin-top: 35px;
  margin-left: 0px;
  color: black;
  background-color: transparent;
}
</style>