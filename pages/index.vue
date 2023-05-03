<template>
  <div id="app">
      <ckeditor :editor="editor" ref="editor" v-model="editorData" :config="editorConfig" @ready="onReady">
      </ckeditor>
      <button @click="click">CLick</button>
  </div>
</template>

<script>
  import HelloWorldButton from '~/components/HelloWorldButton.vue';

  let ClassicEditor = null;
  if (process.browser) {
    ClassicEditor = require('@ckeditor/ckeditor5-build-classic');
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
          editor.ui.componentFactory.add('MyButton', (locale) => {
            const button = document.createElement('button');
            button.type = 'button';
            button.innerText = 'My Button';
            button.addEventListener('click', () => {
              editor.commands.get('myCommand').execute();
            });
            return button;
          });

          console.log(editor);
        },
        click() {
          const editor = this.$refs.editor.$_instance;
          // Create a new button element
          const button = document.createElement('button');
          button.type = 'button';
          button.innerText = 'My Button';
          button.addEventListener('click', () => {
            console.log('Hello');
            // editor.commands.get('myCommand').execute();
          });

          // Insert the button at the current selection position in the editor
          editor.model.change((writer) => {
            const insertPosition = editor.model.document.selection.getFirstPosition();
            writer.insertElement(button, insertPosition);
          });
        },
      },
  }
</script>
