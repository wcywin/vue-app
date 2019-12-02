<template>
    <div>
        <h1>Events Listing</h1>
        <event-card v-for="event in events" :key="event.id" :event="event"/>
        <BaseIcon />
    </div>
</template>

<script>
	import EventCard from '@/components/EventCard'
    import BaseIcon from '@/components/BaseIcon'
    import EventService from '@/services/EventService'

    export default {
        name: "EventList",
        components: {
            BaseIcon,
            EventCard
        },
        data() {
            return {
                events: []
            }
        },
        created() {
            EventService.getEvents()
                .then(response => {
                    this.events = response.data
                })
                .catch(error => {
                    console.log(`There was an error: ${error.response}`)
                })
            }
    }
</script>

<style scoped>

</style>