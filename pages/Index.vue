<template>
  <q-page class="q-pa-xl flex flex-center bg-grey-11">

    <Form @tableUpdate="updateTable" />

    <CountryDetails :entries=results />

  </q-page>
</template>

<script>

import Form from 'components/form.vue'
import CountryDetails from 'components/countrytable.vue'

export default {
  name: 'PageIndex',
  components: { Form, CountryDetails },
  data () {
    return {
      results: []
    }
  },

  methods: {

    updateTable (values) {
      this.results = values
    }
  }
}
</script>
