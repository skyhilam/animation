<template>
	<div>
		<ul class="list">
			<list-item  v-for="i in 20" :key="i">
				List Item {{i}}
			</list-item>
		</ul>
	</div>
</template>


<script>
	import ListItem from '@/components/List/Item'

	export default {
		components: {ListItem}
	}
</script>