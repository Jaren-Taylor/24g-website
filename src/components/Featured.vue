<template>
  <div id="Featured">
    <h3>Featured Videos</h3>
    <hr />
    <li v-for="video in videos" v-bind:key="video.id">
      <h4 v-if="video.show">{{video.title}}</h4>
      <img
        v-if="video.show"
        @click="select_video(video)"
        :src="video.thumb"
        height="100"
        width="150"
      />
    </li>
  </div>
</template>

<script>
export default {
  name: "Featured",
  data: function() {
    return {
      videos: [
        {
          title: "Who is 24G?",
          video:
            "https://static-email-hosting.s3.amazonaws.com/24G_Test_Project/videos/who_is_24g.mp4",
          thumb:
            "https://static-email-hosting.s3.amazonaws.com/24G_Test_Project/videos/who_is_24g.jpg",
          likes: 0,
          dislikes: 0,
          views: 0,
          show: true,
          comments: [],
          id: 1
        },
        {
          title: "CES Overview",
          video:
            "https://static-email-hosting.s3.amazonaws.com/24G_Test_Project/videos/ces_overview.mp4",
          thumb:
            "https://static-email-hosting.s3.amazonaws.com/24G_Test_Project/videos/ces_overview.jpg",
          likes: 0,
          dislikes: 0,
          views: 0,
          show: true,
          comments: [],
          id: 2
        },
        {
          title: "Future of Drones",
          video:
            "https://static-email-hosting.s3.amazonaws.com/24G_Test_Project/videos/future_of_drones.mp4",
          thumb:
            "https://static-email-hosting.s3.amazonaws.com/24G_Test_Project/videos/future_of_drones.jpg",
          likes: 0,
          dislikes: 0,
          views: 0,
          show: true,
          comments: [],
          id: 3
        }
      ]
    };
  },
  props: ["child_video", "comment"],
  watch: {
    child_video: function() {
      this.videos.forEach(element => {
        if (element.title == this.child_video.title) {
          element = this.child_video;
        } else {
          element.show = true;
        }
      });
    },
    comment: function() {
      this.videos.forEach(element => {
        if (element.title == this.child_video.title) {
          element.comments.push(this.comment);
          this.$emit("comment_added", element);
        }
      });
    }
  },
  methods: {
    select_video(video) {
      this.$emit("video_props", video);
    }
  }
};
</script>
<style scoped>
div {
  margin-top: -518px;
  float: right;
}
h3 {
  text-align: left;
  background-color: transparent;
  width: 500px;
}
li {
  list-style-type: none;
}
img:hover {
  opacity: 0.5;
}
</style>