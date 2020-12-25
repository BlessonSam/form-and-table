<template>
    <q-card class="my-card q-pa-xl">

  <q-form
   @submit="onSubmit"
   class="q-pa-md">
      <div class="q-mb-md">
        <span>Full Name</span>
        <q-input outlined v-model="name" ref="fullname"
        :rules="[ val => val && val.length > 2 || 'Please enter a valid name']"
        />
      </div>

      <div class="q-mb-md">
        <span>Email</span>
        <q-input v-model="email" type="email" outlined ref="email"
        :rules="[ val => val && val.length > 3 || 'Please enter an email']"
         bottom-slots
         error-message="Please enter a valid email id"
         />
      </div>

      <div class="q-mb-md">
        <span>Date of Birth</span>
         <q-input v-model="date" outlined type="date" ref="dob"
         :rules="[ val => val && val.length > 9 || 'Please enter a valid date']"
         />
      </div>

      <div class="q-mb-md">
        <span>Region</span>
         <q-select outlined v-model="region" :options="options" ref="region"
         :rules="[ val => val && val.length > 2 || 'Please select a region']"
         />
      </div>

      <div class="q-gutter-sm">
      <q-checkbox
        v-model="agree"
        color="secondary"
        label="I agree to the terms & conditions"
      />
    </div>

    <div class="row justify-end">
      <q-btn
        type="submit"
        :loading="submitting"
        label="Submit"
        class="q-mt-md"
        color="teal"
      >
        <template v-slot:loading>
          <q-spinner-tail
           color="white"
           size="1em"
          />
        </template>
      </q-btn>
    </div>
  </q-form>

    </q-card>

</template>

<script>
export default {
  name: 'Form',
  data () {
    return {
      name: null,
      email: null,
      date: null,
      age: 0,
      agree: false,
      submitting: false,
      region: null,
      options: [
        'Africa', 'Americas', 'Asia', 'Europe', 'Oceania'
      ],
      results: []
    }
  },

  // computed: {
  //  isValidEmail () {
  //   return true
  //  },

  // validAge () {
  // if (this.date.getFullYear() < 2003) {
  //  return true
  //  } else {
  //  return false
  // }
  // }
  // },
  // https://restcountries.eu/rest/v2/region/{region}

  methods: {

    onSubmit () {
      if (this.agree !== true) {
        this.$q.notify({
          color: 'red-5',
          textColor: 'white',
          icon: 'warning',
          message: 'You need to accept the terms and conditions first'
        })
      } else {
        this.submitting = true

        this.$axios.get('https://restcountries.eu/rest/v2/region/' + this.region + '?fields=name;capital;population;area').then((response) => {
          this.results = response.data
        })
          .catch((error) => {
            console.error(error)
          })
        setTimeout(() => {
        // delay simulated, we are done,
        // now restoring submit to its initial state
          this.$emit('tableUpdate', this.results)
          this.submitting = false
          this.$q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            message: 'Submitted'
          })
          this.name = null
          this.email = null
          this.date = null
          this.region = null
          this.agree = false
          this.$refs.fullname.resetValidation()
        }, 3000)
      }
    }
  }
}
</script>
