<template>
  <div id="app">
    <h1>
      Welcome,
      <em>Jaren</em>
    </h1>
    <h2>
      <img alt="24g logo" src="./assets/24g_logo_white.png" height="50" width="100" />
      Video Player
    </h2>
    <Video :video="video_data" v-on:video_loaded="updateVideoList"></Video>
    <Featured
      v-on:video_props="onUpdateVideo"
      :child_video="child_data"
      :comment="comment_data"
      v-on:comment_added="commentUpdated"
    ></Featured>
    <br />
    <br />
    <br />
    <br />
    <Comments
      v-on:new_comment="updateComments"
      :video="video_comment_data"
      v-on:video_loaded="showCurrentComments"
      :curr_video="child_data"
    ></Comments>
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <br />
    <hr />
    <h3>
      <img alt="powered_by_24g" src="./assets/powered_by_24g_white.png" height="37.5" width="200" />
    </h3>
  </div>
</template>

<script>
import Video from "./components/Video.vue";
import Featured from "./components/Featured.vue";
import Comments from "./components/Comments.vue";
export default {
  name: "App",
  components: {
    Video,
    Featured,
    Comments
  },
  data: function() {
    return {
      video_data: "",
      child_data: "",
      comment_data: "",
      video_comment_data: ""
    };
  },
  methods: {
    onUpdateVideo(video) {
      this.video_data = video;
    },
    updateVideoList(child_video) {
      this.child_data = child_video;
    },
    updateComments(comment) {
      this.comment_data = comment;
    },
    commentUpdated(video_comment) {
      this.video_comment_data = video_comment;
    },
    showCurrentComments() {
      this.video_comment_data = this.child_data;
    }
  }
};
</script>

<style>
@font-face {
  font-family: BGR;
  src: url("./assets/24G Programming Test Project/fonts/BRANDON_REG.otf");
}
div {
  font-family: BGR;
}

body {
  background-color: rgb(57, 60, 62);
}

h1 {
  margin-top: -7px;
  margin-left: -8px;
  height: 50px;
  background: rgb(0, 157, 220);
}

h2 {
  margin-top: -21px;
  margin-left: -8px;
  background-color: rgb(6, 133, 194);
  color: white;
}
h3 {
  text-align: center;
}
.vl {
  width: 5px;
  height: 300px;
  border-left: 6px solid rgb(6, 133, 194);
  position: absolute;
  left: 50%;
  margin-left: -3px;
  top: 190px;
}
</style>
