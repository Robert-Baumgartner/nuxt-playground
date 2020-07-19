<template>
  <div>
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
export default {
  async asyncData ({ $axios, error }) {
    try {
      const result = await $axios.get('http://localhost:3000/events')
      return { events: result.data }
    } catch {
      error({ statusCode: 503, message: 'Unable to fetch events!' })
    }
  },
  head () {
    return {
      title: 'Event Listing'
    }
  }
}
</script>
