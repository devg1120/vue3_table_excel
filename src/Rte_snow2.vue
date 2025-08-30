<script setup lang="ts">
import { ref, computed, useTemplateRef, onMounted } from 'vue'

import { QuillEditor } from '@vueup/vue-quill'
import '@vueup/vue-quill/dist/vue-quill.snow.css';
import '@vueup/vue-quill/dist/vue-quill.bubble.css';


let S = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";
let N = 8;
let ID = Array.from(crypto.getRandomValues(new Uint8Array(N))).map((n)=>S[n%S.length]).join('');
console.log(ID);

let editor_id = "q-editor-" + ID;
let editor_sid = "#" + editor_id;
let toolbar_id = "my-toolbar-" + ID;
let toolbar_sid = "#" + toolbar_id;


const qeditor  = useTemplateRef('qeditor')
onMounted(() => {
  qeditor.value.getToolbar().classList.add("ql-dynamic-toolbar");
});

let isFocus = ref(false);

const handleMouseEnter = () => {
  console.log('focus in', editor_id);
  isFocus.value = true;
  console.log(qeditor.value.getToolbar());
  //let editor = qeditor.value.getEditor();
  //editor.value.classList.add("ql-toolbar-show")
  qeditor.value.getEditor().classList.add("ql-toolbar-show");
  let ele = qeditor.value.getToolbar();
  ele.style.display = "inline-block"
};
const handleMouseLeave = () => {
  console.log('focus out', editor_id);
  isFocus.value = false;
  //let editer = qeditor.value.getEditor();
  //editer.value.classList.remove("ql-toolbar-show")
  qeditor.value.getEditor().classList.remove("ql-toolbar-show");
  let ele = qeditor.value.getToolbar();
  ele.style.display = "none"
};

/*
const classObject = computed(() => {  
   if (isFocus.value) {
      return "toolbar-show" ;
   } else {
      return "toolbar-hidden";
   }
});
*/


const content = ref("<h3> test index </h3>");

function get_html() {
   let html = qeditor.value.getHTML();
   console.log(html);

}

function get_content() {
   console.log(content);

}


</script>

<template>
  <!--
  <QuillEditor ref="qeditor" theme="snow"  :class="classObject" v-bind:id="editor_id" v-bind:toolbar="toolbar_sid" 
         @focus="handleMouseEnter" 
         @blur="handleMouseLeave" 
         @mouseenter="handleMouseEnter" 
         @mouseleave="handleMouseLeave" 
  -->
  <!--
  <QuillEditor theme="snow" ref="qeditor"  toolbar="full"   v-bind:id="editor_id" 
        v-model:content="content"  contentType="html"
         @dblclick="handleMouseEnter" 
         @mouseleave="handleMouseLeave" 
  >
  </QuillEditor>
  -->

  <QuillEditor  theme="snow" ref="qeditor"   v-bind:id="editor_id" v-bind:toolbar="toolbar_sid" 
         v-model:content="content"  contentType="html"
         @dblclick="handleMouseEnter" 
         @blur="handleMouseLeave" 
  >
      <template #toolbar>
      <div v-bind:id="toolbar_id" >
          <button class="ql-bold"></button>
          <button class="ql-italic"></button>
          <button class="ql-underline"></button>
          <button class="ql-strike"></button>
      
          <button class="ql-link"></button>
          <button class="ql-image"></button>
      
          <button class="ql-header" value="1"></button>
          <button class="ql-header" value="2"></button>
      
          <button class="ql-list" value="ordered"></button>
          <button class="ql-list" value="bullet"></button>
          <button class="ql-list" value="check"></button>
      
          <button class="ql-script" value="sub"></button>
          <button class="ql-script" value="super"></button>
      
          <button class="ql-indent" value="-1"></button>
          <button class="ql-indent" value="+1"></button>
      
        <select class="ql-color">
           <option value="#000000"></option>
           <option value="#e60000"></option>
           <option value="#ff9900"></option>
           <option value="#ffff00"></option>
           <option value="#008a00"></option>
           <option value="#0066cc"></option>
           <option value="#9933ff"></option>
           <option value="#ffffff"></option>
           <option value="#facccc"></option>
           <option value="#ffebcc"></option>
           <option value="#ffffcc"></option>
           <option value="#cce8cc"></option>
           <option value="#cce0f5"></option>
           <option value="#ebd6ff"></option>
           <option value="#bbbbbb"></option>
           <option value="#f06666"></option>
           <option value="#ffc266"></option>
           <option value="#ffff66"></option>
           <option value="#66b966"></option>
           <option value="#66a3e0"></option>
           <option value="#c285ff"></option>
           <option value="#888888"></option>
           <option value="#a10000"></option>
           <option value="#b26b00"></option>
           <option value="#b2b200"></option>
           <option value="#006100"></option>
           <option value="#0047b2"></option>
           <option value="#6b24b2"></option>
           <option value="#444444"></option>
           <option value="#5c0000"></option>
           <option value="#663d00"></option>
           <option value="#666600"></option>
           <option value="#003700"></option>
           <option value="#002966"></option>
           <option value="#3d1466"></option>
        </select>
      
        <select class="ql-background">
           <option value="#000000"></option>
           <option value="#e60000"></option>
           <option value="#ff9900"></option>
           <option value="#ffff00"></option>
           <option value="#008a00"></option>
           <option value="#0066cc"></option>
           <option value="#9933ff"></option>
           <option value="#ffffff"></option>
           <option value="#facccc"></option>
           <option value="#ffebcc"></option>
           <option value="#ffffcc"></option>
           <option value="#cce8cc"></option>
           <option value="#cce0f5"></option>
           <option value="#ebd6ff"></option>
           <option value="#bbbbbb"></option>
           <option value="#f06666"></option>
           <option value="#ffc266"></option>
           <option value="#ffff66"></option>
           <option value="#66b966"></option>
           <option value="#66a3e0"></option>
           <option value="#c285ff"></option>
           <option value="#888888"></option>
           <option value="#a10000"></option>
           <option value="#b26b00"></option>
           <option value="#b2b200"></option>
           <option value="#006100"></option>
           <option value="#0047b2"></option>
           <option value="#6b24b2"></option>
           <option value="#444444"></option>
           <option value="#5c0000"></option>
           <option value="#663d00"></option>
           <option value="#666600"></option>
           <option value="#003700"></option>
           <option value="#002966"></option>
           <option value="#3d1466"></option>
        </select>
      
        <select class="ql-font">
          <option value="monospace"></option>
          <option value="sans-serif"></option>
          <option value="serif"></option>
        </select>
      
         <button class="custom-button" @click="get_html" >html</button>
         <button class="custom-button" @click="get_content" >content</button>
      
      </div>
    </template>
  </QuillEditor>

</template>

<style >
/*
table td  .rte-editor {
   padding: 0;
   margin:0;
}
*/

table td  .ql-snow.ql-container.ql-toolbar-show {
   height: calc(100% - 60px);
   padding: 0;
   margin:0;
   border :0;
}

table td  .ql-snow.ql-container {
   height: 100% );
   padding: 0;
   margin:0;
   border :0;
}

table td .ql-snow.ql-toolbar button, .ql-snow .ql-toolbar button {
 margin-left: 1;
 margin-right: 0;
 height: 22px;
 width:  20px;
 padding: 3px 5px;
}


.ql-snow.ql-toolbar.ql-dynamic-toolbar {
 display:none;
}

/*
.ql-snow .ql-tooltip {
 display:none;
}
*/

</style>
