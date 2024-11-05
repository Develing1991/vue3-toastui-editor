<script setup lang="ts">
import { onMounted, ref, watch, onUnmounted } from 'vue';
import Editor from '@toast-ui/editor';
import Viewer from '@toast-ui/editor/dist/toastui-editor-viewer';
import '@toast-ui/editor/dist/toastui-editor.css';
import '@toast-ui/editor/dist/toastui-editor-viewer.css';


const props = defineProps({
	modelValue: {
		type: String,
		required: false,
		default: '',
	},
  edit: {
    type: Boolean,
    default: true
  },
  editorConfig: {
    type: String,
    default: ''
  }
});

const emit = defineEmits(['update:modelValue']);
const editor = ref();
const editorValid = ref();
const testHtml = ref();

//작성한 내용 불러와서 html 적용
const testValid = async (e) => {
  // debugger;
	// testHtml.value = await editorValid.value.getHTML()
  // editorValid.value.setHTML('<p>sdfsdds</p>')
  editorValid.value.setMarkdown(`
  >> 2312
  >> 2312
  `)
};
const toggleEditor = async (e) => {
    emit('toggle')
    
};

const editorConfigSet = () => {
  const editorConfig = {
      ...props.editorConfig,
      el: editor.value,
    }
  
		editorValid.value = props.edit ? new Viewer(editorConfig) : new Editor(editorConfig);
}
//마운트될때 Editor 생성
onMounted(() => {
  editorConfigSet()
});
watch(() => props.edit,() => {
  editorConfigSet()
})


</script>

<template>
    <div class="main">
		  <div ref="editor" />		
      <button @click="toggleEditor">toggle Editor</button>
    </div>
</template>

<style scoped>
.main {
  max-width: 70%;
  
}
</style>
