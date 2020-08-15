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
  asyncData({ $axios, error }) {
    return $axios
      .get('http://localhost:4000/events')
      .then((res) => {
        return {
          events: res.data,
        }
      })
      .catch((e) =>
        error({
          statusCode: 503,
          message: 'Unable to fetch events at this time. Please try later',
        })
      )
  },
  head() {
    return {
      title: 'Event Listing',
    }
  },
}
</script>

<style></style>
