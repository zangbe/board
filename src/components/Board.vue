<template>
    <div style="width:1000px">
        <v-data-table :headers="headers" :items="list" class="elevation-4">
            <template v-slot:top>
                <v-toolbar flat color="white">
                    <v-toolbar-title>Board</v-toolbar-title>
                    <v-divider class="mx-4" inset vertical></v-divider>
                    <v-spacer></v-spacer>
                    <v-btn color="primary" @click="onClickNewButton">추가</v-btn>
                </v-toolbar>
            </template>
            <template v-slot:item.actions="{ item }">
            <v-icon
                small
                class="mr-2"
                @click="onClickEditButton(item)"
            >
                mdi-pencil
            </v-icon>
            <v-icon
                small
                @click="onClickDeleteButton(item)"
            >
                mdi-delete
            </v-icon>
            </template>
            <template v-slot:no-data>
                <div>
                    <b>데이터가 없습니다</b>
                </div>
            </template>
        </v-data-table>
        <v-dialog persistent v-model="dialog" max-width="600px">
            <v-card>
                <v-card-title class="headline">팝업</v-card-title>

                <v-card-text>
                    <v-row>
                        <v-col cols="12">
                            <v-text-field
                                label="번호"
                                readonly
                                filled
                                v-model="editedItem.boardNo"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field
                                label="제목"
                                outlined
                                counter
                                v-model="editedItem.title"
                            ></v-text-field>
                        </v-col>
                        <v-col cols="12">
                            <v-textarea
                                outlined
                                name="input-7-4"
                                label="내용"
                                counter
                                v-model="editedItem.content"
                            ></v-textarea>
                        </v-col>
                        <v-col cols="12">
                            <v-text-field
                                label="작성자"
                                filled
                                readonly
                                v-model="editedItem.writer"
                            ></v-text-field>
                        </v-col>
                    </v-row>
                </v-card-text>
                
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn color="green darken-1" text @click="onClickActionButton">Action</v-btn>
                    <v-btn color="green darken-1" text @click="dialog = false">Close</v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </div>
</template>

<script>
export default {
    data() {
        return {
            headers: [
                {text: 'Actions', value: 'actions'},
                {text: '게시글 번호', value: 'boardNo'},
                {text: '제목', value: 'title'},
                {text: '내용', value: 'content'},
                {text: '작성자', value: 'writer'},
            ],
            list: [],
            dialog: false,
            editedItem: {
                boardNo: '',
                title: '',
                content: '',
                writer: ''
            },
            defaultItem: {
                boardNo: '',
                title: '',
                content: '',
                writer: ''
            },
        }
    },

    methods: {

        onClickNewButton() {
            this.dialog = true;
        },

        onClickEditButton(item) {
            this.dialog = true;
            Object.assign(this.editedItem, item);
        },

        onClickDeleteButton(item) {
            console.log('delete item: ', item)
        },

        onClickActionButton() {
            console.log('item: ', this.editedItem)
        },
    },

    created() {

        for(let i = 1; i <= 20; i++) {
            this.list.push(
                {boardNo: i, title: `제목${i}`, content: `내용${i}`, writer: `작성자${i}`}
            )
        }
    },
}
</script>