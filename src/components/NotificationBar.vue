<template>
    <div
            class="notification-bar"
            :class="notificationTypeClass"
    >
        <p>{{ notification.message }}</p>
    </div>
</template>

<script>
    import { mapActions } from 'vuex'

	export default {
		name: "NotificationBarr",
		props: {
			notification: {
				type: Object,
				required: true
			},
		},
        data() {
			return {
				timeout: null
            }
        },
        beforeDestroy() {
			clearTimeout(this.timeout)
		},
		computed: {
			notificationTypeClass() {
				return `-text-${this.notification.type}`
			}
		},
        mounted() {
		    this.timeout = setTimeout(() => this.remove(this.notification), 5000)
        },
        methods: mapActions('notification', ['remove'])
	}
</script>

<style scoped>
    .notification-bar {
        padding: 10px 20px;
        background-color: white;
        box-shadow: 0 3px 6px rgba(0,0,0,0.15);
        z-index: 1000;
    }
</style>