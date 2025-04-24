<script>
export default {
	name: "CardForm",
	data() {
		return {
			show: {
				title: "",
				description: "",
				image: "",
				rating: 0,
				tags: [],
				notes: "",
				color: "#000000",
				releaseDate: "",
			},
			//tagsInput field needed to store input as a string before formatting to array
			tagsInput: "",
			errorMessage: "",
		};
	},
	methods: {
		handleAddShow() {
			this.formatTags();

			if (!this.validateFormFields()) {
				this.errorMessage = "Please fill out the fields correctly.";
				return;
			}
			//emit a copy of the show object instead of the original to prevent accidental mutations in parent
			this.$emit("addShow", { ...this.show });
			this.resetForm();
		},
		formatTags() {
			this.show.tags = this.tagsInput
				.split(",")
				.map((tag) => tag.trim())
				.filter(Boolean);
		},
		validateFormFields() {
			const s = this.show;
			// Only check for non-empty strings and arrays for properties specified in the PEC
			return (
				s.title.length > 0 &&
				s.description.length > 0 &&
				s.image.length > 0 &&
				Array.isArray(s.tags) &&
				s.tags.length > 0 &&
				s.releaseDate.length > 0
			);
		},
		resetForm() {
			this.show = {
				title: "",
				description: "",
				image: "",
				rating: 0,
				tags: [],
				notes: "",
				color: "#000000",
				releaseDate: "",
			};
			this.tagsInput = "";
			this.errorMessage = "";
		},
		handleCloseCardForm() {
			this.$emit("closeCardForm");
		},
	},
	emits: {
		addShow: (show) =>
			show &&
			typeof show === "object" &&
			typeof show.title === "string" &&
			typeof show.description === "string" &&
			typeof show.image === "string" &&
			typeof show.rating === "number" &&
			Array.isArray(show.tags) &&
			typeof show.notes === "string" &&
			typeof show.color === "string" &&
			typeof show.releaseDate === "string",
		closeCardForm: () => true,
	},
};
</script>
<template>
	<section class="section-add">
		<button class="section-add__close" @click="handleCloseCardForm">
			<img src="/src/assets/arrow-right.svg" alt="Close" />
		</button>
		<h2>Add a new show</h2>
		<!-- Prevent default submission of form and instead call method -->
		<form class="form" @submit.prevent="handleAddShow">
			<div class="form-group">
				<label for="title">Title:</label>
				<input type="text" id="title" v-model.trim="show.title" />
			</div>
			<div class="form-group">
				<label for="description">Description:</label>
				<textarea id="description" v-model.trim="show.description"></textarea>
			</div>
			<div class="form-group">
				<label for="image">Image URL:</label>
				<input type="text" id="image" v-model.trim="show.image" />
			</div>
			<div class="form-group">
				<label for="rating">Rating:</label>
				<!-- Restrict values to between 0 and 5 -->
				<input
					type="number"
					id="rating"
					v-model.number="show.rating"
					min="0"
					max="5"
				/>
			</div>
			<div class="form-group">
				<label for="tags">Tags (comma-separated):</label>
				<input type="text" id="tags" v-model.trim="tagsInput" />
			</div>
			<div class="form-group">
				<label for="notes">Notes:</label>
				<textarea id="notes" v-model.trim="show.notes"></textarea>
			</div>
			<div class="form-group">
				<label for="color">Color:</label>
				<input type="color" id="color" v-model="show.color" />
			</div>
			<div class="form-group">
				<label for="releaseDate">Release date:</label>
				<input type="date" id="releaseDate" v-model="show.releaseDate" />
			</div>
			<button class="btn btn--cta" type="submit">Add show</button>
			<p v-if="errorMessage" class="error-msg">{{ errorMessage }}</p>
		</form>
	</section>
</template>
<style scoped>
.section-add {
	width: calc(100% - 40px);
	min-width: 300px;
	margin: 0 auto;
	padding: 20px;
	border-radius: 8px;
	box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	background-color: #393a41;
	color: white;
	position: relative;
}

.section-add__close {
	position: absolute;
	top: 10px;
	right: 10px;
	background-color: white;
	border-radius: 50%;
	border: none;
	cursor: pointer;
	width: 20px;
	height: 20px;
}

form {
	display: grid;
	gap: 10px;
}

.form-group label {
	display: block;
	margin-bottom: 5px;
	font-weight: bold;
}

.form-group input,
.form-group textarea {
	width: 100%;
	box-sizing: border-box;
	padding: 8px;
	border: 1px solid #ccc;
	border-radius: 4px;
}

.form-group input[type="color"] {
	padding: 0;
	height: 40px;
}

.form-group textarea {
	resize: vertical;
}

.btn[type="submit"] {
	width: 100%;
}

.error-msg {
	color: #ff6b6b;
	font-weight: bold;
	margin-bottom: 10px;
}
</style>
