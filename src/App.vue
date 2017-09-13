<template>
  <div id="app">
    <Topbar class="topbar" />
    <main>
      <Editor class="editor" />
      <Preview class="preview" />
    </main>
  </div>
</template>

<script>
import Topbar from './components/Topbar'
import Editor from './components/Editor'
import Preview from './components/Preview'

export default {
  name: 'app',
  components: {
    Topbar,
    Editor,
    Preview
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  height: 100%;
  overflow: hidden;
}

.topbar {
  position: relative;
  z-index: 1;
  box-shadow: 0 0 3px hsla(0,0,0,0.5);
}

main {
  display: flex;
  flex: 1;
  background: #eee;
}

.editor{
  width: 40em;
  margin: 16px 8px 16px 16px;
  background: #fff;
}

.preview{
  flex: 1;
  margin: 16px 16px 16px 8px;
  background: #fff;
}

.icon{
  width: 2em;
  height: 2em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}
</style>
