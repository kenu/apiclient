<template>
  <div>
    <ul>
      <li>
        <button @click="get">get</button>
      </li>
      <li>
        <button @click="post">post</button>
      </li>
      <li>
        <button @click="put">put</button>
      </li>
      <li>
        <button @click="del">delete</button>
      </li>
      <li>
        <form
          id="uploadForm"
          enctype="multipart/form-data"
          action="/api/upload"
          method="post"
          @submit.prevent="upload"
        >
          <input type="text" name="name" value="text-value" />
          <br />
          <input type="file" name="userFile" multiple />
          <input type="submit" value="Upload File" name="submit" />
        </form>
      </li>
    </ul>
    <code id="result"></code>
  </div>
</template>

<script>
import axios from "axios";

const headers = {
  Accept: "application/json",
  "Content-Type": "application/json",
};

export default {
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
    };
  },
  methods: {
    showResult(json) {
      document.getElementById("result").innerHTML = JSON.stringify(json);
    },
    get: function () {
      fetch("http://localhost:3000/api/user/" + 1, {
        method: "GET",
        headers,
      })
        .then(function (response) {
          return response.json();
        })
        .then((json) => {
          this.showResult(json);
        });
    },
    post() {
      axios
        .post("http://localhost:3000/api/user", {
          id: 20,
          name: "hello",
        })
        .then((response) => {
          this.showResult(response.data);
        });
    },
    async put() {
      const result = await axios
        .put("http://localhost:3000/api/user", {
          id: 1,
          name: "world",
        });
      this.showResult(result.data);
    },
    async del() {
      try {
        const result = await axios.delete("http://localhost:3000/api/user");
        this.showResult(result.data);
      } catch (error) {
        this.showResult(error);
      }
    },
    async upload() {
      try {
        const form = document.getElementById('uploadForm');
        const formData = new FormData(form);
        const result = await axios.post("http://localhost:3000/api/upload", formData,
          {
            headers: {
              'Content-Type': 'multipart/form-data'
            }
          });
        this.showResult(result.data);
      } catch (error) {
        this.showResult(error);
      }
    },
  },
};
</script>
