<template>
    <div id="bookmarks">
        <h3>Bookmarks the Spot:</h3>
        <div v-if="!bookmarks.length">
               <h4>You need to add some bookmarks!</h4>
        </div>

        <draggable v-model="bookmarks" @start="drag=true" @end="drag=false">
            <BookmarkEditor v-for="(bookmark, index) in bookmarks"
                            :key="bookmark"
                            :idx=index
                            :bookmark="bookmark"
                            :on-delete="handleDelete"
                            :on-save="handleSave"
                            :on-create="handleCreate"
            />
        </draggable>

        <input type="text"
               placeholder="Paste a bookmark here."
               v-model="newURL"
               @keyup.enter="handleCreate()"/>

        <Modal v-if="validationError"
               v-bind:message="validationError"
               :on-close="handleModalClose"
        />
    </div>
</template>

<script>
    import Modal from './common/Modal';
    import BookmarkEditor from "./BookmarkEditor";
    import {isValidURL} from "../utils/validation";
    import {EventBus} from "../event-bus";
    import draggable from 'vuedraggable'

    export default {
        name: "BookMarks",
        components: {Modal, BookmarkEditor, draggable},
        data() {
            return {
                newURL: null,
                validationError: null,
                bookmarks: []
            }
        },
        beforeMount() {
            EventBus.$on('escape-clicked', () => this.validationError = null);
            //Check to see if we have some bookmarks already otherwise set to an empty array.
            this.bookmarks = JSON.parse(localStorage.getItem('bookmarks')) || [];
        },
        methods: {
            handleDelete(bookmark) {
                this.bookmarks = this.bookmarks.filter(obj => obj !== bookmark)
            },
            updateBookMarks(bookmark, idx) {
                let bookmarks = [...this.bookmarks];
                (idx < 0)? bookmarks.push(bookmark): bookmarks[idx] = bookmark;
                this.bookmarks = bookmarks;
                this.newURL = null;
            },
            handleSave(bookmark, idx) {
                if(this.bookmarks.indexOf(bookmark) >= 0) {
                    this.validationError = `This url exists already:<br><strong style="padding-left: 40px">${bookmark}</strong>`;
                }
                else if (!isValidURL(bookmark)) {
                    this.validationError = `There is an error in your url:<br><strong style="padding-left: 40px">${this.newURL}</strong>`;
                }
                else {
                    this.updateBookMarks(bookmark,idx);
                }
            },
            handleCreate() {
                this.handleSave(this.newURL, -1);
            },
            handleModalClose() {
                this.validationError = null;
            },
        },
        watch: {
            bookmarks: function (bookmarks) {
                localStorage.setItem('bookmarks', JSON.stringify(bookmarks));
            }
        }
    }
</script>

<style lang="scss">
    #bookmarks {
        display: flex;
        flex-direction: column;
        align-items: stretch;
        background-color: white;
        padding: 20px;
        border-radius: 8px;
    }
</style>

