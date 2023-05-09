<template>
  <div id="app">
      <ckeditor :editor="editor" ref="editor" v-model="editorData" :config="editorConfig" @ready="onReady">
      </ckeditor>
      <button @click="click">CLick</button>
  </div>
</template>

<script>
  let ClassicEditor = null;
  if (process.browser) {
    ClassicEditor = require('@hieu1311/ckeditor5-build-classic');
  }
  export default {
      name: 'app',
      data() {
          return {
              editor: ClassicEditor,
              editorData: 'hehhhehe',
              editorConfig: {
                  // The configuration of the editor.
              }
          };
      },

      methods: {
        onReady(editor) {
          console.log(editor);
        },
        click() {
          const editor = this.$refs.editor.$_instance;
          editor.execute( 'placeholder', { value: 'time' } );
        },
      },
  }
</script>
