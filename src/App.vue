<template>
  <div>
    <CustomEditor :edit="edit" :editor-config="editorConfig" @toggle="toggleEdit" />
  </div>
</template>

<script setup lang="ts">

import CustomEditor from './components/CustomEditor.vue'
import CustomViewer from './components/CustomViewer.vue'
import { ref, reactive } from 'vue';
const edit = ref(false);

const editorConfig = {
			// el: editor.value,
      previewStyle: 'vertical', // tab
			height: '500px',
      //'wysiwyg', 'markdown' 택 1
			initialEditType:  'markdown',
      initialValue: '## content', // ...res.data
      // toolbarItems: [],
			events: {
				change: () => {
          emit('update:modelValue', editorValid.value.getMarkdown())
          console.log(editorValid.value.getMarkdown()); // value
          
          
        }
			},
		}

const toggleEdit = () => {
  edit.value = !edit.value
}
</script>

<style scoped>

</style>