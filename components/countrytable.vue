<template>

    <div class="q-pa-md" style="width:90%">
    <q-table
      :dense="$q.screen.lt.md"
      title="Country Details"
      :data=this.entries
      :columns="columns"
      row-key="name"
    />

  </div>

</template>

<script>
export default {
  name: 'CountryTable',
  props: ['entries'],
  data () {
    return {
      columns: [
        {
          name: 'name',
          required: true,
          label: 'Nation',
          align: 'left',
          field: row => row.name,
          format: val => `${val}`,
          sortable: true
        },
        { name: 'capital', align: 'center', label: 'capital', field: 'capital' },
        { name: 'population', label: 'Population', field: 'population' },
        { name: 'area', label: 'Area (sqkm)', field: 'area' }
      ],
      data: [
        {
          name: 'American Samoa',
          capital: 'Pago Pago',
          population: '57100',
          area: '199'
        }
      ]
    }
  }

}
</script>
