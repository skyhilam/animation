<template>
	<li class="grid-x">
		<div class="cell auto list-item" :class="{show: more}">
			<div><slot /></div>
		</div>
		<transition name="slide">
			<div class="cell list-button list-button-1" v-if="more">
				<span>edit</span>
			</div>
		</transition>
		<div class="cell list-button list-button-1" @click.prevent="toggle">
			<span v-if="more">></span>
			<span v-else>...</span>
		</div>
	</li>
</template>

<script>
	import anime from 'animejs'
	import $ from 'jquery'

	export default {
		data() {
			return {
				more: false,
				item: null,
				button: null
			}
		},
		methods: {
			toggle() {
				this.more = !this.more
				// if (this.more) this.hide()
				// else this.show()
			},
			show() {

				const animetion = anime({
					targets: this.item,
					'margin-left': { value: -this.button.width(), duration: 1200 }
				})

				animetion.begin = () => {
					this.more = true
				}

			},
			hide() {
				const animetion = anime({
					targets: this.item,
					'margin-left': [
						{ value: 0, duration: 1200 }
				    ]
				})

				animetion.begin = () => {
					this.more = false
				}
			}
		},

		mounted() {
			this.item = $(this.$el).find('.list-item>div')[0]
			this.button = $(this.$el).find('.list-button-1')
		}
	}
</script>