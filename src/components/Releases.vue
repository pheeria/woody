<template>
  <q-list>
    <q-item-label header>Latest Releases</q-item-label>

    <q-item v-for="release in data" :key="release.tag" clickable v-ripple>
      <q-item-section side>
        <q-avatar rounded size="48px">
          <img :src="release.avatarUrl" />
        </q-avatar>
      </q-item-section>
      <q-item-section>
        <q-item-label>{{release.release}}</q-item-label>
        <q-item-label caption>{{release.tag}} by {{release.user}}</q-item-label>
      </q-item-section>
      <q-item-section side>{{release.date}}</q-item-section>
    </q-item>
  </q-list>
</template>

<script>
export default {
  name: 'Releases',
  props: ['data']
}
</script>