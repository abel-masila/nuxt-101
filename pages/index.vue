<template>
  <div class="">
    <h1>Events</h1>
    <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
  </div>
</template>

<script>
import EventCard from '~/components/EventCard'
export default {
  components: {
    EventCard,
  },
  async asyncData({ $axios, error }) {
    try {
      const { data } = await $axios.get('http://localhost:4000/events')
      return {
        events: data,
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events events at this time',
      })
    }
  },
  head() {
    return {
      title: 'Event Listing',
    }
  },
}
</script>

<style></style>
