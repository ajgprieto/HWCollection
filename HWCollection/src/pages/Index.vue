<template>
  <q-page>
    <q-table
      grid
      hide-header
      :data="cars"
      :columns="carsHeader"
      row-key="name"
      :rows-per-page-options="[0]"
      :pagination.sync="paginationControl"
      hide-bottom="true"
      :filter="filter"
      >
        <template slot="top" slot-scope="props">
          <q-search hide-underline clearable v-model="filter" />
        </template>
        <div
          slot="item"
          slot-scope="props"
          class="q-pa-xs col-xs-12 col-sm-6 col-md-4 transition-generic"
          :style="props.selected ? 'transform: scale(0.95);' : ''"
        >
          <q-card
            class="transition-generic cursor-pointer"
            :class="props.selected ? 'bg-grey-2' : ''"
          >
            <q-card-title class="relative-position">
              {{ props.row.nameOnCard }}
            </q-card-title>
            <q-card-separator />
            <q-card-main class="q-pa-none">
              <q-list>
                <q-item>
                  <q-item-side>
                    Brand
                  </q-item-side>
                  <q-item-main>
                    {{ props.row.brand }}
                  </q-item-main>
                </q-item>
                <q-item>
                  <q-item-side>
                    Model
                  </q-item-side>
                  <q-item-main>
                    {{ props.row.model }}
                  </q-item-main>
                </q-item>
                <q-item>
                  <q-item-side>
                    Color
                  </q-item-side>
                  <q-item-main>
                    {{ props.row.color }}
                  </q-item-main>
                </q-item>
                <q-item>
                  <q-item-side>
                    Series
                  </q-item-side>
                  <q-item-main>
                    {{ props.row.series }}
                  </q-item-main>
                </q-item>
                <q-item>
                  <q-item-side>
                    Card Number
                  </q-item-side>
                  <q-item-main>
                    {{ props.row.cardNumber }}
                  </q-item-main>
                </q-item>
                <q-item>
                  <q-item-side>
                    Quantity
                  </q-item-side>
                  <q-item-main>
                    {{ props.row.quantity }}
                  </q-item-main>
                </q-item>
              </q-list>
            </q-card-main>
          </q-card>
        </div>
      </q-table>
  </q-page>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',
  data() {
    return {
      filter: null,
      paginationControl: {
        rowsPerPage: 300
      },
      carsHeader: [
        {
          name: 'brand',
          label: 'Brand',
          align: 'center',
          field: 'brand'
        },
        {
          name: 'cardNumber',
          label: 'Card Number',
          align: 'center',
          field: 'cardNumber'
        },
        {
          name: 'color',
          label: 'Color',
          align: 'center',
          field: 'color'
        },
        {
           name: 'Model',
           label: 'Model',
           align: 'center',
           field: 'model'
         },
         {
           name: 'NameOnCard',
           label: 'Name on Card',
           align: 'center',
           field: 'nameOnCard'
         },
         {
           name: 'Quantity',
           label: 'Quantity',
           align: 'center',
           field: 'quantity'
         },
         {
           name: 'Series',
           label: 'Series',
           align: 'center',
           field: 'series'
         },
      ],
      cars: [],
      batman: [],
      other: []
    }
  },
  created: function() {
    this.$axios.get('https://raw.githubusercontent.com/ajgprieto/HWCollection/master/HWCollection/src/data/cars.json')
      .then((carsList) => {
        this.cars = carsList.data;
        console.log(this.cars);
      })
      .catch(() => {
        this.$q.notify({
          message: 'Unable to retrieve cars list.'
        })
      })
  }
}
</script>
