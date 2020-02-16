<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md">
      <q-table
        class="my-sticky-header-table"
        :data="data"
        :columns="columns"
        :pagination.sync="customPagination"
        row-key="name"
        flat
        bordered
      />
    </div>
  </q-page>
</template>

<script>
export default {
  name: 'Deployments',
  props: ['data'],
  data() {
    return {
      columns: [
        {
          name: 'country',
          required: true,
          label: 'Country',
          align: 'left',
          field: 'country',
          sortable: true
        },
        {
          name: 'b2c',
          align: 'center',
          label: 'B2C',
          field: row => row.b2c.tag,
          sortable: true
        }
      ],
      customPagination: {
        rowsPerPage: 0,
        sortBy: 'country'
      }
    }
  }
}
</script>

<style lang="scss">
.my-sticky-header-table {
  /* height or max-height is important */
  height: 85vh;
  width: 75vw;

  .q-table__top,
  .q-table__bottom,
  thead tr:first-child th {
    /* bg color is important for th; just specify one */
    background-color: #d70f64;
    font-weight: bolder;
  }
  thead th {
    color: white;
  }

  thead tr th {
    position: sticky;
    z-index: 1;
  }
  thead tr:first-child th {
    top: 0;
  }
  /* this is when the loading indicator appears */
  &.q-table--loading thead tr:last-child th {
    /* height of all previous header rows */
    top: 48px;
  }
}
</style>

