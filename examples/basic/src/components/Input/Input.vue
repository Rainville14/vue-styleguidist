<template>
	<div>
		<input ref="input" v-model="val" @input="updateValue($event.target.value)" @change="emitChange" />
		<button @click="fireEvent()">
			Fire example event!
		</button>
	</div>
</template>

<script>
export default {
	name: 'Input',
	model: {
		prop: 'value'
	},
	props: {
		value: {
			default: null,
			type: [Number, String]
		},
		/**
		 * Using for: String.prototype.replace(regexp, replacement)
		 */
		regExp: {
			type: RegExp,
			default: null
		},
		/**
		 * Using for: String.prototype.replace(regexp, replacement)
		 */
		replacement: {
			type: String,
			default: ''
		}
	},
	data() {
		return {
			val: ''
		}
	},
	watch: {
		// watch value prop
		value(val) {
			this.updateValue(val)
		}
	},
	mounted() {
		this.updateValue(this.value)
	},
	methods: {
		// format the value of input
		formatValue(val) {
			const formattedValue = !val ? '' : val.toString().replace(this.regExp, this.replacement)

			return formattedValue
		},

		updateValue(val) {
			const formattedValue = this.formatValue(val)

			this.val = formattedValue
			this.emitInput(formattedValue)
		},

		emitInput(val) {
			/**
			 * Input event
			 * @event input
			 * @type {number|string}
			 * @property {number} called - test called
			 * @property {boolean} isPacked - Indicates whether the snowball is tightly packed.
			 */
			this.$emit('input', val, 1, false)
		},

		// emit change event
		emitChange() {
			/**
			 * Change event
			 * @event change
			 */
			this.$emit('change', this.val)
		},
		fireEvent() {
			/**
			 * Fire event
			 * @event fire
			 * @type {string}
			 */
			this.$emit('fire', 'hello fire!!')
		}
	}
}
</script>

<style></style>
