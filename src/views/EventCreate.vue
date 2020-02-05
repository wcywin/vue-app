<template>
    <div>
        <h1>Create an Event</h1>

        <form @submit.prevent="createEvent">
            <BaseSelect
                label="Select a category"
                :options="categories"
                v-model="event.category"
            />
            <h3>Name & describe your event</h3>
            <BaseInput
                class="field"
                label="Title"
                type="text"
                placeholder="Add an event title"
                v-model="event.title"
            />
            <BaseInput
                class="field"
                label="Description"
                type="text"
                placeholder="Add a description"
                v-model="event.description"
            />
            <h3>Where is your event?</h3>
            <BaseInput
                class="field"
                label="Location"
                type="text"
                placeholder="Add a location"
                v-model="event.location"
            />
            <h3>When is your event?</h3>
            <div class="field">
                <label>Date</label>
                <datepicker v-model="event.date" placeholder="Select a date"/>
            </div>
            <BaseSelect
                label="Select a time"
                :options="times"
                v-model="event.time"
                :class="field"
            />
<!--            <input type="submit" class="button -fill-gradient" value="Submit"/>-->
            <BaseButton
                type="submit"
                button-class="-fill-gradient"
            >
                Submit
            </BaseButton>
        </form>
    </div>

</template>

<script>
    import Datepicker from 'vuejs-datepicker'
    import NPrograss from 'nprogress'
	import BaseInput from '../components/BaseInput'
	import BaseSelect from '../components/BaseSelect'
	import BaseButton from '../components/BaseButton'

	export default {
		name: "EventCreate",
        components: {
			BaseButton,
			BaseSelect,
			BaseInput,
			Datepicker
		},
        data() {
			const times = []
            for (let i = 1; i <= 24; i++) {
            	times.push(i + ':00')
            }
			return {
				times,
                categories: this.$store.state.categories,
				event: this.createFreshEventObject()
            }
        },
        methods: {
			createEvent() {
				NPrograss.start()
                this.$store
                    .dispatch('event/createEvent', this.event)
                    .then(() => {
                    	this.$router.push({
                            name: 'event-show',
                            params: { id: this.event.id }
                        })
					this.event = this.createFreshEventObject()
                }).catch(() => {
                    NPrograss.done()
                })
            },
			createFreshEventObject() {
				const user = this.$store.state.user.user
                const id = Math.floor(Math.random() * 10000000)

                return {
					id: id,
                    user: user,
					category: '',
                    organizer: user,
                    title: '',
					description: '',
					time: '',
					date: '',
					location: '',
                    attendees: []
                }
            }
        }
	}
</script>

<style scoped>
    .field {
        margin-bottom: 24px;
    }
</style>