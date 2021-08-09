<template>
    <v-card max-width="200  " >
        <v-img
        class="white--text align-end"
        height="200"
        :src="image"
        >
        </v-img>
        <v-card-title>{{title}}</v-card-title>
    </v-card>
</template>
<script>
export default {
  name: 'card',
  props: [
    'title',
    'image'
  ]
}
</script>
