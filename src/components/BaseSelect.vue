<template>
    <div>
        <label v-if="label">
            {{ label }}
        </label>
        <select
            v-on="$listeners"
            :value="value"
            @change="updateValue"
            v-bind="$attrs"
        >
            <option
                v-for="option in options"
                :value="option"
                :key="option"
                :selected="option === value"
            >
                {{ option }}
            </option>
        </select>
    </div>
</template>

<script>
	import { formFieldMixin } from '../mixins/formFieldMixin'

	export default {
		name: "BaseSelect",
		mixins: [ formFieldMixin ],
		props: {
			options: {
				type: Array,
                required: true
            }
		}
	}
</script>

<style scoped></style>