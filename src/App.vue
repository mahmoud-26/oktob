<template>
  <div ref="container">
    <nav class="navbar">
      <div class="buttons">
        <i class="fi fi-br-b" @click="b"></i>
        <i class="fi fi-br-i" @click="i"></i>
        <i class="fi fi-br-h" @click="h"></i>
        <i class="fi fi-br-picture" @click="g"></i>
        <i class="fi fi-br-quote-right" @click="q"></i>
        <i class="fi fi-br-code-simple" @click="c"></i>
        <i class="fi fi-br-link-alt" @click="l"></i>
        <i class="fi fi-br-list" @click="u"></i>
        <!--
        <i class="fi fi-br-expand" @click="toggleFullscreen" v-if="!fullscreen"></i>
        <i class="fi fi-br-compress" @click="toggleFullscreen" v-if="fullscreen"></i>
        -->
      </div>
      <div class="toggle">
        <i class="fi fi-br-eye" v-if="!show" @click="toggle"></i>
        <i class="fi fi-br-pen-clip" v-if="show" @click="toggle"></i>
      </div>
    </nav>
    <div class="editor">
      <textarea ref="textarea" dir="rtl" v-model="value" class="textarea" @input="update" placeholder="قم بالكتابة هنا..."></textarea>
      <div dir="rtl" class="output" v-html="output" v-if="show"></div>
    </div>
  </div>
</template>

<script>
  import { marked } from 'marked'

  export default {
    data() {
      return {
        value: '',
        show: true,
        fullscreen: false
      }
    },
    mounted() {
      if (localStorage.getItem("text") == null) {
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
      /*
      toggleFullscreen() {
        this.fullscreen = !this.fullscreen
        let container = this.$refs.container
        if (this.fullscreen) {
          if (container.requestFullscreen) {
            container.requestFullscreen();
          } else if (container.webkitRequestFullscreen) {
            container.webkitRequestFullscreen();
          } else if (container.msRequestFullscreen) {
            container.msRequestFullscreen();
          }
        } else {
          if (document.exitFullscreen) {
            document.exitFullscreen();
          } else if (document.webkitExitFullscreen) {
            document.webkitExitFullscreen();
          } else if (document.msExitFullscreen) {
            document.msExitFullscreen();
          }
        }
      },
      */
      b() {
        let textarea = this.$refs.textarea
        const sentence = textarea.value
        const len = sentence.length
        let pos = textarea.selectionStart
        const before = sentence.substr(0, pos)
        const after = sentence.substr(pos, len)
        this.value = before + "****" + after
        localStorage.setItem("text", this.value)
      },
      i() {
        let textarea = this.$refs.textarea
        const sentence = textarea.value
        const len = sentence.length
        let pos = textarea.selectionStart
        const before = sentence.substr(0, pos)
        const after = sentence.substr(pos, len)
        this.value = before + "__" + after
        localStorage.setItem("text", this.value)
      },
      h() {
        let textarea = this.$refs.textarea
        const sentence = textarea.value
        const len = sentence.length
        let pos = textarea.selectionStart
        const before = sentence.substr(0, pos)
        const after = sentence.substr(pos, len)
        this.value = before + "# " + after
        localStorage.setItem("text", this.value)
      },
      g() {
        let textarea = this.$refs.textarea
        const sentence = textarea.value
        const len = sentence.length
        let pos = textarea.selectionStart
        const before = sentence.substr(0, pos)
        const after = sentence.substr(pos, len)
        this.value = before + "![]()" + after
        localStorage.setItem("text", this.value)
      },
      q() {
        let textarea = this.$refs.textarea
        const sentence = textarea.value
        const len = sentence.length
        let pos = textarea.selectionStart
        const before = sentence.substr(0, pos)
        const after = sentence.substr(pos, len)
        this.value = before + ">" + after
        localStorage.setItem("text", this.value)
      },
      c() {
        let textarea = this.$refs.textarea
        const sentence = textarea.value
        const len = sentence.length
        let pos = textarea.selectionStart
        const before = sentence.substr(0, pos)
        const after = sentence.substr(pos, len)
        this.value = before + "``````" + after
        localStorage.setItem("text", this.value)
      },
      l() {
        let textarea = this.$refs.textarea
        const sentence = textarea.value
        const len = sentence.length
        let pos = textarea.selectionStart
        const before = sentence.substr(0, pos)
        const after = sentence.substr(pos, len)
        this.value = before + "[]()" + after
        localStorage.setItem("text", this.value)
      },
      u() {
        let textarea = this.$refs.textarea
        const sentence = textarea.value
        const len = sentence.length
        let pos = textarea.selectionStart
        const before = sentence.substr(0, pos)
        const after = sentence.substr(pos, len)
        this.value = before + "*" + after
        localStorage.setItem("text", this.value)
      }
    }
  }
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Lateef:wght@200;300;400;500;600;700;800&display=swap');

  @font-face {
    font-family: 'hafs';
    src: url('fonts/hafs.ttf');
  }

  :root {
    --blue: #0077B6;
    --black: rgb(31, 41, 55);
    --white: #FFFFFF;
    --yellow: rgb(253, 241, 207);
  }

  * {
    box-sizing: border-box;
  }

  body {
    padding: 0;
    margin: 0;
    width: 100%;
    height: 100vh;
  }

  .navbar {
    width: 100%;
    height: 50px;
    background: var(--black);
    position: fixed;
    top: 0;
    left: 0;
    z-index: 999;
    border-bottom-left-radius: 10px;
    border-bottom-right-radius: 10px;
  }

  .buttons {
    width: 80%;
    height: 50px;
    padding: 9px;
    display: flex;
    justify-content: space-around;
    /*
    display: grid;
    row-gap: 5px;
    column-gap: 35px;
    grid-template-columns: repeat(4, 1fr);
    grid-template-rows: repeat(2, 1fr);
    */
  }

  .buttons i {
    font-size: 0.85em;
    color: var(--white);
    padding: 10px;
    border-radius: 5px;
    transition: background 0.1s;
  }

  .buttons i:active {
    background: #023E8A;
  }

  .toggle i {
    font-size: 1.2em;
    color: var(--white);
    position: absolute;
    top: 16px;
    right: 30px;
  }

  .textarea,
  .output code,
  .output p,
  .output a,
  .output h1,
  .output h2,
  .output h3,
  .output h4,
  .output h5,
  .output h6,
  .output table {
    font-family: 'lateef' !important;
  }

  .textarea {
    width: 100%;
    height: 100vh;
    padding: 2.8em 1.1em 2em 1.1em !important;
    font-size: 1.7em;
    border: none;
    outline: none;
    font-weight: 400;
    color: var(--black);
  }

  .output {
    width: 100%;
    height: 100vh;
    font-size: 1.7em;
    padding: 1.8em 1.1em 1em 1.1em;
    position: absolute;
    top: 0;
    left: 0;
    background: var(--white);
    overflow-x: hidden;
    overflow-y: auto;
    font-weight: 400;
    color: var(--black);
  }

  .output img {
    width: 100%;
    border-radius: 5px;
  }

  .output blockquote {
    font-family: 'hafs' !important;
    padding: 0 0.05em;
    margin: 0;
    border-right: 3px solid var(--black);
    background: whitesmoke;
    border-radius: 5px;
  }
  
  .output blockquote p {
    font-family: 'hafs' !important;
  }

  .output code {
    color: var(--white);
    background: var(--black);
    padding: 0.1em 0.5em;
    border-radius: 5px;
  }

  .output a {
    text-decoration: none;
    color: var(--blue);
  }

  .output h1,
  .output h2,
  .output h3,
  .output h4 {
    font-weight: 800;
  }

  .output h5,
  .output h6 {
    font-weight: 600;
  }

  .output table {
    margin: 1em 0;
    width: 100%;
    border: 1px solid var(--black);
    border-radius: 4px;
    text-align: center;
  }

  .output table td,
  .output table th {
    padding: 5px;
    border: 0.5px solid var(--black);
    border-radius: 2px;
  }
</style>