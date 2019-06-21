<template>
  <div class="editor-wrap">
    <p class="btn-wrap">
      <button @click="execCommand('bold')">加粗</button>
      <button @click="execCommand('italic')">斜体</button>
      <button @click="execCommand('underline')">下划线</button>
      <button @click="execCommand('backColor','pink')">背景色</button>
      <button @click="execCommand('foreColor','red')">字体颜色</button>
      <button @click="execCommand('formatBlock', '<p>')">段落</button>
      <button @click="insertLink">插入链接</button>
      <button class='img-btn' @click="selectImg">插入图片
        <input class="file-input" ref="fileImg" type="file" accept="image/gif, image/jpeg, image/png" @change="insertImg" >
      </button>
    </p>
    <div class="editor-scan">
      <div class="editor-item editor" contenteditable="true" ref="editor" @input="change"></div>
      <div class="editor-item scan">{{originalTxt}}</div>
    </div>
    <p class="tip">核心方法：<a href="https://developer.mozilla.org/zh-CN/docs/Web/API/Document/execCommand" target="_blank"><b>document.execCommand</b></a></p>
  </div>
</template>

<script>
export default {
  name: 'richInput',
  data(){
    return {
      originalTxt:'',
      imgUrl: ''
    }
  },
  props: {
    msg: String
  },
  methods:{
    execCommand(name, args = null){
      document.execCommand(name, false, args)
    },
    change(){
      this.originalTxt = this.$refs.editor.innerHTML
    },
    selectImg(){
      this.$refs.fileImg.click()
    },
    insertLink(){
      let url = prompt("请输入链接","")
      this.execCommand("createLink", url)
    },
    insertImg(){
      let fileReader = new FileReader()
      let file = event.target.files[0]
      fileReader.onload = ()=>{
        let base64Img = fileReader.result
        this.execCommand("insertImage", base64Img)
      }
      fileReader.readAsDataURL(file)
    }
  },
  mounted(){
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.editor-wrap{
  display: inline-block;
  padding: 40px;
  border: 1px solid gray;
  margin: 20px auto;
}
.btn-wrap{
  display: flex;
}
.editor-scan{
  display: flex;
}
.editor-item{
  width: 400px;
  height: 400px;
  padding: 20px;
  text-align: left;
  font-size: 20px;
  word-wrap: break-word;
  border: 1px solid black;
  overflow: hidden;
  overflow-y: auto;
}
.editor{
  margin-right: 30px;
}
.img-btn{
  display: inline-flex;
  justify-content: center;
  align-items: stretch;
}
.file-input{
  flex: auto;
  display: none;
}
</style>
