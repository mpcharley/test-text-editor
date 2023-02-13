<template>
  <div class="editor-wrapper">
    <div class="editor-toolbar">
      <editor-button @click="undo">
        <template #icon>
          <icon-undo></icon-undo>
        </template>
      </editor-button>
      <editor-button @click="redo">
        <template #icon>
          <icon-redo></icon-redo>
        </template>
      </editor-button>
      <editor-button @click="applyHeading">
        <template #icon>
          <icon-heading></icon-heading>
        </template>
      </editor-button>
      <editor-button @click="clear">
        <template #icon>
          <icon-paragraph></icon-paragraph>
        </template>
      </editor-button>
      <editor-button @click="insertImage">
        <template #icon>
          <icon-image></icon-image>
        </template>
      </editor-button>
      <div @click="copy" class="blue">Скопировать HTML</div>
    </div>
    <div class="editor-content">
      <div
          class="editor"
          ref="editor"
          @input="onInput"
          contenteditable="true"
          v-html="editorContent"
      ></div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref, defineProps, defineEmits } from 'vue';
import EditorButton from './EditorButton.vue';
import IconUndo from './icons/IconUndo.vue';
import IconRedo from './icons/IconRedo.vue';
import IconHeading from './icons/IconHeading.vue';
import IconParagraph from './icons/IconParagraph.vue';
import IconImage from './icons/IconImage.vue';

const props = defineProps({
  modelValue: { type: String, default: '' },
});

const emit = defineEmits(['update:modelValue']);
const editorContent = ref('');
const editor = ref(null);
function undo() {
  document.execCommand('undo');
}
function redo() {
  document.execCommand('redo');
}
function clear() {
  document.execCommand('formatBlock', false, '<p>');
}
function applyHeading() {
  document.execCommand('formatBlock', false, '<h4>');
}
function insertImage() {
  let img = prompt('Введите URL картинки');
  if (img) {
    document.execCommand('insertHtml', false, '<br>');
    document.execCommand('insertImage', false, img);
  }
}
function onInput() {
  emit('update:modelValue', editor.value.innerHTML);
}

function copy(){
  navigator.clipboard.writeText(editor.value.innerHTML);
  alert("HTML Скопирован в буфер обмена");
}

onMounted(() => {
  document.execCommand('defaultParagraphSeparator', false, 'p');
  editorContent.value = props.modelValue;
});

</script>

<style lang="scss">
@import "@/assets/main.scss";

.editor-wrapper {
  background: $darker;
  min-height: 100vh;

  .editor-toolbar {
    display: flex;

    .blue {
      padding-top: 7px;
      margin-left: 10px;
      color: $blue;
      cursor: pointer;
    }
  }

  .editor-content {
    background: $darker;
    padding: 10px;

    .editor {
      text-align: left;
      font-family: "Roboto";
      font-style: normal;
      font-weight: 400;
      font-size: 15px;
      line-height: 23px;
      color: $grey;
      margin: 10px;
      padding: 10px;
      border: none !important;
      outline: none;

      img {
        margin-top: 10px;
        margin-bottom: 10px;
      }

      h4 {
        margin-top: 10px;
        margin-bottom: 10px;
        font-size: 31px !important;
        line-height: 23px !important;
        color: white !important;
      }
    }
  }
}
</style>
