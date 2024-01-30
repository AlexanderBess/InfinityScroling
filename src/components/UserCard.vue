<template>
	<div class="card">
		<img :src="user.picture.large" :alt="`${user.name.first} ${user.name.last}`" />
		<div class="card__info">
			<h3>Full name: {{user.name.first}} {{user.name.last}}</h3>
			<p>Email: {{ user.email }}</p>
		</div>
	</div>
</template>
<script setup>
defineProps({
  user: Object
})
</script>

<style scoped>
.card {
	display: flex;
	flex-direction: column;
	align-items: center;
	width: -webkit-fill-available;
	gap: 10px;
	padding: 15px;

	background-color: rgba(104, 117, 134, 0.623);
	border-radius: 12px;

	img {
		width: max-content;
		border: 1px solid rgba(233, 233, 233, 0.658);
		border-radius: 8px;
	}

	.card__info {
		display: flex;
		flex-direction: column;
		gap: 8px;
	}
}
</style>    