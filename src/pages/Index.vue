<template>
  <q-page class="flex-center q-pa-md">
    <q-card class="my-card" style="min-height: 450px">
      <q-card-section>
        <div class="row">
          <div class="col q-pr-md">
            <q-input type="number" :min="0" rounded outlined v-model="no_of_rows" label="No. Of Rows" />
          </div>
          <div class="col">
            <q-input rounded outlined v-model="columns_string" label="Columns String" />
          </div>
        </div>
        <div class="row q-pt-md">
          <div class="col q-pr-md">
            <q-input type="number" :min="0" rounded outlined v-model="gutter_row" label="Space between rows" />
          </div>
          <div class="col">
            <q-input type="number" :min="0" rounded outlined v-model="gutter_col" label="Space between boxes" />
          </div>
        </div>
        <span class="q-pa-md" v-if="parseInt(no_of_rows)>0">
          <div v-for="(n,index) in parseInt(no_of_rows)" :key="index">
            <div class="row" v-bind:style="{ margin: calcMarginRow(gutter_row)}" v-if="parseInt(columns_arr[index])">
              <div class="col" v-for="(col, key) in parseInt(columns_arr[index])" :key="key">
                <div class="box" v-bind:style="{ margin: calcMarginCol(gutter_col)}"></div>
              </div>
            </div>
            <div class="text-center q-pt-md text-h6" v-else>Enter no.of columns for row {{index+1}}</div>
          </div>
        </span>
        <h6 class="text-center" v-else>Please enter no.of rows</h6>
        <Row />
        <Box />
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>

export default {
  name: 'PageIndex',
  data () {
    return {
      no_of_rows: '',
      columns_string: '',
      gutter_row: '',
      gutter_col: '',
      num_of_cols: '',
      columns_arr: ''
    }
  },
  watch: {
    columns_string: function (newCol, oldCol) {
      this.columns_arr = this.columns_string.split(',')
    }
  },
  methods: {
    calcMarginCol (col) {
      let wi = (col) / (2) + 'px'
      let margin = '0px ' + wi
      return margin
    },
    calcMarginRow (row) {
      let wi = (row) / (2) + 'px'
      let margin = wi + ' 0px'
      return margin
    }
  }
}
</script>

<style scoped>
.box {
  background: rgba(86,61,124,.15);
  border: 1px solid rgba(86,61,124,.2);
  height: 50px;
}
</style>
