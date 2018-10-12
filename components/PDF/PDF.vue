<template>
	<div class="pdf-document">
		<PDFPage 
			v-for="page in pages" 
			v-bind="{page, scale}"
	    	:key="page.pageNumber" />
	</div>
</template>

<script>
	import PDFPage from '@/components/PDFPage'
	import {range} from 'lodash'
	import pdfjs from 'pdfjs-dist'
	import $ from 'jquery'

	export default {
		components: {PDFPage},
		props: {
			src: {
				type: String,
				default: ''
			}
		},
		data() {
			return {
				pdf: null,
				pages: [],
				scale: 2
			}
		},
		mounted() {
			pdfjs
				.getDocument(this.src)
				.then(pdf => {
					this.pdf = pdf
				})
		},
		watch: {
			pdf(pdf) {
				this.pages = []
				const promises = range(1, pdf.numPages)
					.map(number => pdf.getPage(number))

				Promise.all(promises)
					.then(pages => (this.pages = pages))
			}
		}
	}
</script>