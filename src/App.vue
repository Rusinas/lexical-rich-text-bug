<template>
  <div class="wrapper">
    <h1>Lexical bug</h1>
    <div id="editor" contenteditable="true" />
  </div>
</template>

<script setup lang="ts">
import { onMounted } from 'vue'

import {
    createEditor,
    type CreateEditorArgs,
} from 'lexical'

import {
    registerRichText,
} from '@lexical/rich-text'

const EMPTY_STATE = '{"root":{"children":[{"children":[],"direction":null,"format":"","indent":0,"type":"paragraph","version":1}],"direction":null,"format":"","indent":0,"type":"root","version":1}}'

const config: CreateEditorArgs = {
    editable: true,
    namespace: 'editorie',
    theme: {
        paragraph: 'editor-paragraph'
    },
    onError: console.error
};

const editor = createEditor(config)

const parsed_state = editor.parseEditorState(EMPTY_STATE)

editor.setEditorState(parsed_state)

registerRichText(editor)

onMounted(() => {
    editor.setRootElement(document.getElementById('editor'));
})
</script>

<style>
.wrapper {
  display: grid;
  gap: 20px;
}
#editor {
  width: 800px;
  background-color: #f7f7f7; 
}
</style>



