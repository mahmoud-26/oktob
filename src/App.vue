<template>
  <nav class="navbar">
    <i class="fi fi-rr-eye eye" v-if="!show" @click="toggle"></i>
    <i class="fi fi-rr-letter-case pen" v-if="show" @click="toggle"></i>
  </nav>
  <div class="editor">
    <textarea dir="rtl" v-model="value" class="textarea" @input="update"></textarea>
    <div dir="rtl" class="output" v-html="output" v-if="show"></div>
  </div>
</template>

<script>
import { marked } from 'marked'

export default {
  data() {
    return {
      value: '',
      show: true
    }
  },
  mounted() {
    if (localStorage.getItem("text") == null) {
      localStorage.setItem("text", "# Hello")
      this.value = localStorage.getItem("text")
    } else {
      this.value = localStorage.getItem("text")
    }
  },
  computed: {
    output() {
      return marked(this.value)
    }
  },
  methods: {
    update() {
      localStorage.setItem("text", this.value)
    },
    toggle() {
      this.show = !this.show
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=IBM+Plex+Sans+Arabic:wght@100;200;300;400;500;600;700&display=swap');
  :root {
    --blue: #0077B6;
    --black: rgb(31, 41, 55);
    --white: #FFFFFF;
    --yellow: rgb(253, 241, 207);
  }
  * {
    box-sizing: border-box;
    font-family: 'IBM Plex Sans Arabic', sans-serif;
  }
  body {
    padding: 0;
    margin: 0;
    width: 100%;
    height: 100vh;
  }
  .navbar {
    width: 100%;
    height: 60px;
    background: white;
    background: var(--blue);
    position: relative;
  }
  .eye {
    font-size: 1.4em;
    color: ghostwhite;
    position: absolute;
    top: 17px;
    right: 30px;
  }
  .pen {
    font-size: 1.6em;
    color: ghostwhite;
    position: absolute;
    top: 17px;
    right: 30px;
  }
  .textarea {
    width: 100%;
    height: 100vh;
    padding: 1em 1.5em;
    font-size: 1em;
    border: none;
    outline: none;
  }
  .output {
    width: 100%;
    height: auto;
    padding: 0.2em 1.5em 1em 1.5em;
    padding-bottom: 20px !important;
    position: absolute;
    top: 60px;
    left: 0;
    background: var(--white);
  }
  .output img {
    width: 100%;
    border-radius: 5px;
  }
  .output blockquote {
    padding: 0.01px 0.5em;
    margin: 0;
    border-right: 3px solid var(--blue);
    background: var(--yellow);
    border-radius: 5px;
  }
  .output code {
    color: var(--white);
    background: var(--black);
    padding: 0.5em;
    border-radius: 5px;
  }
</style>