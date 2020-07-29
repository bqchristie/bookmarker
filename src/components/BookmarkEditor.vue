<template>
    <div class="bookmark-editor">
        <img class="btn" src="images/edit.png" @click="toggleEdit()"/>
        <img class="btn" src="images/trash.png" @click="onDelete(bookmark)"/>
        <a target="_blank" v-if="!editable" :href="bookmark">{{bookmark}}</a>
        <input v-show="editable"
               type="text"
               ref="bookMarkInput"
               v-model="localBookmark"
               @keyup.enter="toggleEdit();onSave(localBookmark,idx)"
               @blur="toggleEdit()"
        />
    </div>
</template>
<script>

    export default {
        name: 'BookmarkEditor',
        props: {
            bookmark: {type: String},
            idx: {type: Number},
            onDelete: {type: Function,},
            onSave: {type: Function},
        },
        data() {
            return {
                editable: false,
                localBookmark: this.bookmark
            }
        },
        methods: {
            toggleEdit() {
                this.editable = !this.editable;
                this.$nextTick(() => {
                    if (this.editable && this.$refs['bookMarkInput']) {
                        this.$refs['bookMarkInput'].focus();
                    }
                });

            }
        }
    }
</script>
<style lang="scss">
    .bookmark-editor {
        display: flex;
        flex-direction: row;
        margin-bottom: 10px;
        height: 40px;

        input {
            flex: 1;
        }
    }
</style>
