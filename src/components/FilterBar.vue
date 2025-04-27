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
	emits: ["showCardForm"],
	methods: {
		handleAddShowClick() {
			this.$emit("showCardForm");
		},
	},
};
</script>

<template>
	<div class="filter-bar">
		<div class="filter-bar__first">
			<input type="text" placeholder="Search" />
			<button class="btn">Clear</button>
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
				<select id="tag-filter">
					<option v-for="tag in tags" :key="tag" :value="tag">{{ tag }}</option>
				</select>
			</div>
			<div class="input-group">
				<label for="rating-filter">Min rating</label>
				<input type="range" id="rating-filter" min="0" max="5" value="0" />
			</div>
			<div class="input-group">
				<label for="sort-filter">Sort by</label>
				<select id="sort-filter">
					<option value="name">Name</option>
					<option value="date">Release</option>
					<option value="rating">Rating</option>
				</select>
			</div>
			<div class="input-group">
				<label for="order-filter">Order</label>
				<select id="order-filter">
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
