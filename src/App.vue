<template>
  <nav class="navbar">
    <div class="buttons">
      <i class="fi fi-br-b" @click="b"></i>
      <i class="fi fi-br-i" @click="i"></i>
      <i class="fi fi-br-h" @click="h"></i>
      <i class="fi fi-rr-picture" @click="g"></i>
    </div>
    <div class="toggle">
      <i class="fi fi-rr-eye" v-if="!show" @click="toggle"></i>
      <i class="fi fi-rr-edit" v-if="show" @click="toggle"></i>
    </div>
  </nav>
  <div class="editor">
    <textarea ref="textarea" dir="rtl" v-model="value" class="textarea" @input="update"></textarea>
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
    },
    b() {
      let textarea = this.$refs.textarea
      const sentence = textarea.value
      const len = sentence.length
      let pos = textarea.selectionStart
      const before = sentence.substr(0, pos)
      const after = sentence.substr(pos, len)
      this.value = before + "****" + after
    },
    i() {
      let textarea = this.$refs.textarea
      const sentence = textarea.value
      const len = sentence.length
      let pos = textarea.selectionStart
      const before = sentence.substr(0, pos)
      const after = sentence.substr(pos, len)
      this.value = before + "__" + after
    },
    h() {
      let textarea = this.$refs.textarea
      const sentence = textarea.value
      const len = sentence.length
      let pos = textarea.selectionStart
      const before = sentence.substr(0, pos)
      const after = sentence.substr(pos, len)
      this.value = before + "# " + after
    },
    g() {
      let textarea = this.$refs.textarea
      const sentence = textarea.value
      const len = sentence.length
      let pos = textarea.selectionStart
      const before = sentence.substr(0, pos)
      const after = sentence.substr(pos, len)
      this.value = before + "![]()" + after
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
  .buttons {
    width: 80%;
    height: 60px;
    padding-top: 6px;
    display: flex;
    justify-content: space-around;
    align-items: center;
  }
  .buttons i {
    font-size: 1em;
    color: var(--white);
  }
  .toggle i {
    font-size: 1.2em;
    color: var(--white);
    position: absolute;
    top: 19px;
    right: 30px;
  }
  .textarea {
    width: 100%;
    height: 100vh;
    padding: 1.2em 1.5em;
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