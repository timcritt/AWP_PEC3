<script>
export default {
	props: {
		cardFormVisible: {
			type: Boolean,
			default: false,
		},
		tags: {
			type: Array,
			default: () => [],
		},
	},
	name: "FilterBar",
	emits: ["showCardForm", "inputsUpdated"],
	data() {
		return {
			// Defining the input values as nested properties of an object allows setting a single watcher on all inputs.
			// Due to their interdependcy, all filters must be applied to the unfiltered (full) list of shows everytime one of them changes,
			// so using a single watcher means less code duplication and easier extension in the future. You only need to add the new input
			// to the inputs object, connect it to the new input element with v-model, and the watcher will handle changes.
			inputs: {
				searchTerm: "",
				selectedTag: "",
				sortBy: "name",
				sortOrder: "asc",
				minRating: 0,
			},
		};
	},
	watch: {
		// The deep option is set to true to watch for changes in nested properties.
		// A watcher is more suitable than firing an event for each input change, as it keeps the template cleaner.
		inputs: {
			handler(newInputs) {
				// Emit a copy of the inputs object to avoid mutating the original object in the parent component.
				this.$emit("inputsUpdated", { ...newInputs });
				console.log("Inputs updated:", newInputs);
			},
			deep: true,
		},
	},
	methods: {
		handleAddShowClick() {
			this.$emit("showCardForm");
		},
		resetInputs() {
			this.inputs = {
				searchTerm: "",
				selectedTag: "",
				sortBy: "name",
				sortOrder: "asc",
				minRating: 0,
			};
		},
	},
};
</script>

<template>
	<div class="filter-bar">
		<div class="filter-bar__first">
			<input type="text" placeholder="Search" v-model="inputs.searchTerm" />
			<button class="btn" @click="resetInputs">Clear</button>
			<button
				class="btn btn--cta"
				v-if="!cardFormVisible"
				@click="handleAddShowClick"
			>
				Add new show
			</button>
		</div>
		<div class="filter-bar__second">
			<div class="input-group">
				<label for="tag-filter">Tag</label>
				<select id="tag-filter" v-model="inputs.selectedTag">
					<!-- Empty string for value means this filter will not be activated for the default value -->
					<option value="">All</option>
					<option v-for="tag in tags" :key="tag" :value="tag">{{ tag }}</option>
				</select>
			</div>
			<div class="input-group">
				<label for="rating-filter">Min rating</label>
				<input
					type="range"
					id="rating-filter"
					min="0"
					max="5"
					value="0"
					v-model="inputs.minRating"
				/>
			</div>
			<div class="input-group">
				<label for="sort-filter">Sort by</label>
				<select id="sort-filter" v-model="inputs.sortBy">
					<option value="name">Name</option>
					<option value="date">Release</option>
					<option value="rating">Rating</option>
				</select>
			</div>
			<div class="input-group">
				<label for="order-filter">Order</label>
				<select id="order-filter" v-model="inputs.sortOrder">
					<option value="asc">Ascending</option>
					<option value="desc">Descending</option>
				</select>
			</div>
		</div>
	</div>
</template>

<style scoped>
/* Parent */
.filter-bar {
	display: grid;
	grid-template-rows: 1fr 1fr;
	height: 100px;
	gap: 20px;
	box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	background-color: #393a41;
	border-radius: 10px;
	padding: 10px;
	width: calc(100% - 20px);
	color: white;
	margin-bottom: 20px;
}

/* First column */
.filter-bar__first {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	gap: 10px;
	height: 100%;
}

/* Second column */
.filter-bar__second {
	display: flex;
	flex-direction: row;
	flex-wrap: nowrap;
	gap: 20px;
}

/* Input with label */
.input-group {
	display: flex;
	flex-direction: row;
	gap: 10px;
	align-items: center;
}
</style>
