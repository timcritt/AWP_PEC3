<script>
import ShowCard from './ShowCard.vue';

export default {
	name: 'CardBoard',
	components: {
		ShowCard
	},
	props: {
		showList: {
			type: Array,
			required: true
		}
	}
}
</script>

<template>
	<section class="board">
		<ShowCard v-for="show in showList" :key="show.id" :show="show" />
	</section>
</template>

<style scoped>
.board {
	border-radius: 10px;
	display: grid;
	grid-template-columns: repeat(auto-fit, minmax(275px, 1fr));
	grid-auto-rows: min-content;
	gap: 20px;
}
</style>