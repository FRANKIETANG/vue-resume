<template>
  <div id="app" v-bind:class="{previewMode:previewMode}">
    <Topbar class="topbar" v-on:preview="enterPreview"/>
    <main>
      <Editor class="editor" v-bind:resume="resume"/>
      <Preview class="preview" v-bind:resume="resume"/>
    </main>
    <el-button id="exit-preview" v-on:click="exitPreview">退出预览</el-button>
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
  },
  methods: {
    enterPreview(){
      this.previewMode = true
    },
    exitPreview(){
      this.previewMode = false
    }
  },
  data() {
    return {
      previewMode: false,
      resume: {
        profile: {
          name: '游戏的王者',
          city: '木叶村',
          title: '我要成为海贼王的男人',
          birth: '1995-12-30'
        },
        workHistory: [
          {
            company: '美国白宫',
            content: '搞死了记者和自己提拔的州长，怼走了总统，从党鞭当上了总统'
          },
          {
            company: '房车',
            content: '我有个名字叫 Heisenberg，搞死了所有的竞争对手，New Mexico 最大的毒枭'
          }
        ],
        studyHistory: [
          {
            school: 'House of Black and White',
            degree: '高中',
            duration: 'No one know'
          }
        ],
        projects: [
          {
            name: '可口可乐广告',
            content: '离开了 BBDO，消失了3个月创造了脍炙人口的广告歌《everyday》'
          }
        ],
        awards: [
          {
            name: 'Pied Piper的核心和算法',
            content: '以破纪录的压缩成绩获得了冠军'
          }
        ],
        contacts: [
          {
            phone: '123',
            qq: '456',
            wechat: '789',
            email: '1234567'
          }
        ]
      }
    }
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
  box-shadow: 0 0 3px hsla(0, 0, 0, 0.5);
}

main {
  display: flex;
  flex: 1;
  background: #eee;
}

.editor {
  width: 40%;
  margin: 16px 8px 16px 16px;
  background: #fff;
}

.preview {
  flex: 1;
  margin: 16px 16px 16px 8px;
  background: #fff;
}

.icon {
  width: 2em;
  height: 2em;
  vertical-align: -0.15em;
  fill: currentColor;
  overflow: hidden;
}

.previewMode #topbar{
  display: none;
}

.previewMode #editor{
  display: none;
}

.previewMode #preview{
  max-width: 800px;
  margin: 10px auto;
}

#exit-preview {
  display: none;
}

.previewMode #exit-preview{
  display: block;
  position: fixed;
  right: 20px;
  bottom: 20px;
}
</style>
