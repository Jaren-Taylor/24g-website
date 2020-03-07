<template>
  <div id="comment_section">
    <hr />
    <h3>Comment Section</h3>
    <div id="input_form">
      <input
        id="input_box"
        type="text"
        placeholder="Speak your mind!"
        @keyup.enter="updateComments"
      />
      <button @click="updateComments()">Post</button>
      <hr />
    </div>
    <li id="comments" v-for="comment in comments" v-bind:key="comment.id">
      <div id="single_comment">
        <span id="comment_date">comment posted on {{comment.date}}</span>
        <h4 id="comment_text">{{comment.content}}</h4>
        <hr />
      </div>
    </li>
  </div>
</template>

<script>
export default {
  name: "Comments",
  data: function() {
    return {
      comments: [],
      video_title: ""
    };
  },
  props: ["video", "curr_video"],
  watch: {
    curr_video: function() {
      this.comments = this.curr_video.comments;
    }
  },
  methods: {
    updateComments() {
      console.log('here');
      var today = new Date();
      var dd = String(today.getDate()).padStart(2, "0");
      var mm = String(today.getMonth() + 1).padStart(2, "0"); //January is 0!
      var yyyy = today.getFullYear();

      today = mm + "/" + dd + "/" + yyyy;
      var comment = {
        date: "",
        content: "",
        id:''
      };
      comment.content = document.getElementById("input_box").value;
      comment.date = today;
      comment.id = Date.now();
      if (comment.content != "") {
        document.getElementById("input_box").value = "";
        this.$emit("new_comment", comment);
      }
    }
  }
};
</script>
<style scoped>
li {
  list-style-type: none;
}
hr {
  border-color: rgb(6, 133, 194);
}
input {
  border-radius: 25px;
  border: 2px solid rgb(209,209,209);
  padding: 20px;
  width: 200px;
  background-color:rgb(235,235,235);
}
button {
  background-color: rgb(57,60,62);
  border-radius:12px;
  padding: 10px;
  text-align: center;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px 0px 10px;
  color: rgb(235,235,235);
}
button:hover{
    opacity: 0.5;
    background-color: rgb(209,209,209);
    color:rgb(57,60,62);
}
</style>