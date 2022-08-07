<div class="editor-panel">
  <div class="preview"><slot name="preview" /></div>
  <div class="panel"><slot /></div>
</div>

<style>
  .editor-panel {
    display: flex;
  }
  .preview {
    flex: 1;
  }
  .panel {
    flex-shrink: 0;
    padding: 10px;
  }
</style>
