<template>
  <div class="hello-world-button" @click="onClick">
    Hello World
  </div>
</template>

<script>
export default {
  methods: {
    onClick() {
      const editor = this.$parent.editor;
      editor.model.change(writer => {
        const position = editor.model.document.selection.getFirstPosition();
        writer.insertText('Hello World', position);
      });
    }
  }
};
</script>

<style>
.hello-world-button {
  cursor: pointer;
  background-color: #f7f7f7;
  padding: 5px 10px;
  border-radius: 3px;
  display: inline-block;
  margin-right: 10px;
}
</style>
