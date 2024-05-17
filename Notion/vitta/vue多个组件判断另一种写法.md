```Dart
<template>
  <component :is="modeComponent" : />
</template>
<script>
import Affiliate from './affiliate/index'
import Analytics from './analytics/index'
import Common from './common/index'
import PageMixin from '../../mixins/PageMixin'
export default {
  mixins: [PageMixin], data () { return { title: 'Dashboard', modes: { affiliate: Affiliate, analytics: Analytics, common: Common } } }, computed: { user () { return this.$store.state.User }, mode () { return this.user.dashboard || 'common' }, modeComponent () { return this.modes[this.mode] } }
}
</script>
<style lang="scss"></style>
```