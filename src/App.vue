<template>
  <div id="app">
    <router-view />
    <back-to-top :visibility-height="100" :back-position="0" transition-name="fade" ref="backTop"/>
    <mindex v-if="$route.meta.showFooter"></mindex>
  </div>

</template>

<script>

import BackToTop from '@/components/BackToTop'
import mindex from './layout/m_index'

export default {
  name: 'App',
  components: {
    mindex,
    BackToTop
  }
}
</script>
