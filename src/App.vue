<template>
	<div class="notes-app">
		<notes-header :title="title" />
		<notes-editor @createNote="createNote" />
		<notes-grid :notes="notes" />
	</div>
</template>

<script>
	import NotesHeader from '@/components/NotesHeader.vue';
	import NotesEditor from '@/components/NotesEditor.vue';
	import NotesGrid from '@/components/NotesGrid.vue';

	const notes = localStorage.notes ? JSON.parse(localStorage.notes) : [];

	export default {
		name: 'notes-app',

		components: {
			NotesHeader,
			NotesEditor,
			NotesGrid,
		},

		data: () => ({
			title: 'Нотатник by Khalimon',
			notes,
		}),

		methods: {
			findNotes(tagsArr) { 
				alert('da');
				this.notes = this.notes.filter(note => {
					let inArr = false;
					tagsArr.forEach(element => {
						if(note.includes(element)) inArr = true;
					});
					return inArr;
				 });
				 console.log(this.notes.length);
			},

			createNote(note) {
				this.notes.push(note);
				localStorage.notes = JSON.stringify(this.notes);
			},

			deleteNote(id) {
				this.notes = this.notes.filter(note => note.id !== id);
				localStorage.notes = JSON.stringify(this.notes);
			},

			editNote() {
				localStorage.notes = JSON.stringify(this.notes);
			},
		},
	};
</script>

<style lang="scss">
	$color: #eabcd5;

	* {
		box-sizing: border-box;
	}

	body {
		font-family: sans-serif;
		font-weight: 300;
		background-color: $color;
	}

	.notes-app {
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
		max-width: 980px;
		margin: 0 auto;
	}
</style>
