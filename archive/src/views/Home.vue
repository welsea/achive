<template>
  <div class="home">
    <UserInfo />
    <Timeline />
  </div>
</template>

<script>
// @ is an alias to /src
import Timeline from '@/components/Timeline.vue'
import UserInfo from '@/components/UserInfo.vue'


export default {
  name: 'Home',
  components: {
    Timeline,
    UserInfo
  }
}
</script>
