<template>
  <div>
    <div class="layout-padding" style="max-width: 500px">
      <router-link tag="a" to="/layout-quick/a" class="cursor-pointer row justify-center" style="margin-bottom: 25px">
        <img src="statics/quasar-logo.png">
      </router-link>
      <div
        class="list no-border"
        v-for="(category, title) in list"
        :key="`category-${title}`"
      >
        <h4 class="uppercase">
          {{ title }}
        </h4>
        <q-item
          v-for="feature in category"
          :key="`${feature.route}${feature.title}`"
          :to="feature.route"
        >
          <q-item-main :label="feature.title" />
          <q-item-side right icon="chevron_right" />
        </q-item>
      </div>
    </div>
  </div>
</template>

<script>
import pages from '../pages'

let list = {}
pages.map(page => page.slice(0, page.length - 4)).forEach(page => {
  let [folder, file] = page.split('/')
  if (!list[folder]) {
    list[folder] = []
  }
  list[folder].push({
    route: page,
    title: file.charAt(0).toUpperCase() + file.slice(1)
  })
})

export default {
  data () {
    return {
      list
    }
  }
}
</script>
