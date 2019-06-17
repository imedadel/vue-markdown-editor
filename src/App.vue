<template>
	<div id="app">
		<!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
		<!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
		<textarea :value="input" @input="update" class="border-none border-r border-solid border-gray-400"></textarea>
		<div v-html="compiledMarkdown"></div>
	</div>
</template>

<script>
import marked from 'marked'
import debounce from 'lodash.debounce'

export default {
	name: 'app',
	data: function() {
		return {
			input: '# hello',
		}
	},
	computed: {
		compiledMarkdown: function() {
			return marked(this.input, { sanitize: true })
		},
	},
	methods: {
		update: debounce(function(event) {
			this.input = event.target.value
		}, 300),
	},
}
</script>

<style>
html,
body,
#app {
	margin: 0;
	height: 100%;
	font-family: 'Helvetica Neue', Arial, sans-serif;
	color: #333;
}

textarea,
#app div {
	display: inline-block;
	width: 49%;
	height: 100%;
	vertical-align: top;
	box-sizing: border-box;
	padding: 0 20px;
}

textarea {
	resize: none;
	outline: none;
	background-color: #f6f6f6;
	font-size: 14px;
	font-family: 'Monaco', courier, monospace;
	padding: 20px;
}

code {
	color: #f66;
}
</style>
