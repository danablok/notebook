<template>
    <div class="note" :style="{ backgroundColor: note.bgcolor }">
		<span class="edit-note" :style="{ display: note.edit ? 'block' : 'none' }"
              @click="showInput(note, false, $parent.$parent)">
			✓
		</span>
        <span class="delete-note" @click="$parent.$parent.deleteNote(note.id)">
			x
		</span>
        <span @click="showInput(note, true)">
			<!-- <input v-model="note.text" 
				type="text" 
				size="18" 
				:placeholder="[[ note.text ]]"
				:disabled="note.edit ? false:true"
			> -->
			<textarea :rows="note.text.length/18+1" cols="18" name="text"
                      v-model="note.text"
                      type="text"
                      size="18"
                      :placeholder="[[ note.text ]]"
                      :disabled="note.edit ? false:true"
            />
		</span>
    </div>
</template>

<script>
    export default {
        name: 'note-item',
        props: {
            note: {
                type: Object,
                required: true,
                edit: false
            },
        },

        methods: {
            showInput(note, show, parent = null) {
                note.edit = show;
                if (parent) {
                    parent.editNote();
                }
                //alert(note.edit);
            }
        },
    };
</script>

<style lang="scss" scoped>
    .note {
        width: 200px;
        height: auto;
        float: left;
        box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
        border-radius: 2px;
        padding: 10px;
        margin-bottom: 10px;
        transition: box-shadow 0.3s;
        word-wrap: break-word;
        position: relative;
    }

    .note:hover {
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.19), 0 6px 6px rgba(0, 0, 0, 0.23);
    }

    .edit-note {
        position: absolute;
        top: 3px;
        right: 20px;
        display: none;
        color: rgba(0, 0, 0, 0.6);
        cursor: pointer;
    }

    .delete-note {
        position: absolute;
        top: 5px;
        right: 5px;
        display: none;
        color: rgba(0, 0, 0, 0.6);
        cursor: pointer;
    }

    .note:hover .delete-note {
        display: block;
    }

    .note:hover .edit-note {
        display: block;
    }

    .hide {
        display: none;
    }
</style>
