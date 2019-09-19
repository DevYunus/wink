<script type="text/ecmascript">
    import _ from 'lodash';
    import Quill from 'quill';

    export default {
        components: {},

        props: {
            value: {
                type: String,
                default: ''
            }
        },

        data() {
            return {
                editor: null,
                editorBody: this.body
            }
        },


        mounted() {
            this.editor = this.createEditor();

            this.handleEditorValue();
        },


        /**
         * Clean after the component is destroyed.
         */
        destroyed() {
        },


        methods: {
            /**
             * Create an instance of the editor.
             */
            createEditor() {
                return new Quill(this.$refs.editor, {
                    modules: {
                        syntax: true,
                        toolbar: [
                      //      ['bold', 'italic', 'underline', 'strike', 'link'],
//                        [{'direction': 'rtl'}],
['bold', 'italic', 'underline', 'strike'],        // toggled buttons
  ['blockquote', 'code-block'],

  [{ 'header': 1 }, { 'header': 2 }],               // custom button values
  [{ 'list': 'ordered'}, { 'list': 'bullet' }],
  [{ 'script': 'sub'}, { 'script': 'super' }],      // superscript/subscript
  [{ 'indent': '-1'}, { 'indent': '+1' }],          // outdent/indent
  [{ 'direction': 'rtl' }],                         // text direction

  [{ 'size': ['small', false, 'large', 'huge'] }],  // custom dropdown
  [{ 'header': [1, 2, 3, 4, 5, 6, false] }],

  [{ 'color': [] }, { 'background': [] }],          // dropdown with defaults from theme
  [{ 'font': [] }],
  [{ 'align': [] }],

  ['clean']
                        ]
                    },
                    theme: 'bubble',
                    scrollingContainer: 'html, body'
                });
            },


            /**
             * Handle the editor value.
             */
            handleEditorValue() {
                this.editor.root.innerHTML = this.value || 'Write something...';

                this.editor.on('text-change', () => {
                    this.$emit('input', this.editor.getText() ? this.editor.root.innerHTML : '');
                });
            }
        }
    }
</script>

<template>
    <div class="relative">
        <div ref="editor"></div>
    </div>
</template>

<style scoped>
    .ql-container {
        font-size: inherit;
    }
</style>
