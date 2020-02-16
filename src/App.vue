<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar class="panda">
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          aria-label="Menu"
          icon="ion-menu"
        />
        <q-toolbar-title>Woody</q-toolbar-title>

        <a
          class="github"
          href="https://github.com/pheeria/woody"
          target="_blank"
          rel="noopener noreferrer"
        >
          <q-icon name="ion-logo-github" size="32px"></q-icon>
        </a>
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" show-if-above bordered content-class="bg-grey-2">
      <Releases :data="releases" />
    </q-drawer>

    <q-page-container>
      <Deployments :data="deployments" />
    </q-page-container>
  </q-layout>
</template>

<script>
import Releases from './components/Releases.vue'
import Deployments from './components/Deployments.vue'

export default {
  name: 'LayoutDefault',

  components: {
    Deployments,
    Releases
  },

  methods: {
    initReleases() {
      fetch(`${process.env.VUE_APP_WOODPECKER}/wood`, {
        method: 'POST'
      })
        .then(res => res.json())
        .then(res => {
          this.releases = res
        })
    },
    fetchDeployments() {
      fetch(`${process.env.VUE_APP_WOODPECKER}/peck`, {
        method: 'POST'
      })
        .then(res => res.json())
        .then(res => {
          this.deployments = res
        })
    }
  },

  data() {
    return {
      leftDrawerOpen: false,
      fetching: null,
      interval: 1000,
      deployments: [],
      releases: []
    }
  },

  created() {
    this.fetchDeployments()
    this.initReleases()

    this.fetching = setInterval(() => {
      this.fetchDeployments()
    }, this.interval)
  },

  beforeDestroy() {
    clearInterval(this.fetching)
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=Montserrat+Alternates&display=swap');
*,
body,
html {
  font-family: 'Montserrat Alternates', sans-serif;
  font-weight: 700;
}
.panda {
  background-color: #d70f64;
}
.github {
  &:link,
  &:visited,
  &:hover,
  &:active {
    color: white;
    text-decoration: none;
  }
}
</style>
