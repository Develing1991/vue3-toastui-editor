<script setup lang="ts">
import { onMounted, ref, watch, onUnmounted } from 'vue';
import Editor from '@toast-ui/editor';
import '@toast-ui/editor/dist/toastui-editor.css';

const props = defineProps({
	modelValue: {
		type: String,
		required: false,
		default: '',
	},
});

const emit = defineEmits(['update:modelValue']);
const editor = ref();
const editorValid = ref();
const testHtml = ref();

//작성한 내용 불러와서 html 적용
const testValid = (e) => {
	testHtml.value = editorValid.value.getHTML()
};

//마운트될때 Editor 생성
onMounted(() => {
		editorValid.value = new Editor({
			el: editor.value,
      previewStyle: 'vertical',
			height: '500px',
      //'wysiwyg', 'markdown' 택 1
			initialEditType: 'markdown',
			events: {
				change: () => {
          emit('update:modelValue', editorValid.value.getMarkdown())
          console.log(editorValid.value.getMarkdown()); // value
          
        }
			},
		});
});


</script>

<template>
    <div class="main">
		  <div ref="editor" />		
    </div>
</template>

<style scoped>
.main {
  max-width: 70%;
  
}
</style>
