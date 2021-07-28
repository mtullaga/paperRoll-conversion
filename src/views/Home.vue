<template>
  <div id="home" class="container" style="margin-bottom: 20px; font-family: Poppins">
      <b-row class="justify-content-md-center">
        <b-col cols="6">
          <div class="form-group">
            <label class="float-left" style="margin-left: 0px"><b>Select Conversion</b></label>
            <select class="form-control" v-model="selectConversion" 
            @change="changeSelection($event)" style="font-weight: bold">

              <option value="0">All</option>
              <option value="1">Pallet Weight Calculator</option>
              <option value="2">Reel Length Calculator From Dimension</option>
              <option value="3">Reel Length Calculator From Weight</option>
              <option value="4">Reel Diameter Calculator From Length</option>
              <option value="5">Reel Weight Calculator From Dimension</option>
              <option value="6">Reel Weight Calculator After Diameter Reduction</option>
            </select>
          </div>
        </b-col>

        <PalletWeightCalculator v-if="selectConversion == 1 || selectConversion == 0"/>

        <ReelLengthCalculatorFromDimension v-if="selectConversion == 2 || selectConversion == 0"/>

        <ReelLengthCalculatorFromWeight v-if="selectConversion == 3 || selectConversion == 0"/>

        <ReelDiameterCalculatorFromLength v-if="selectConversion == 4 || selectConversion == 0"/>

        <ReelWeightCalculatorFromDimension v-if="selectConversion == 5 || selectConversion == 0"/>

        <ReelWeightCalculatorAfterDiameterReduction v-if="selectConversion == 6 || selectConversion == 0"/>

        
        

      </b-row>
  </div>
</template>

<script>
import PalletWeightCalculator from '../components/PalletWeightCalculator.vue'
import ReelLengthCalculatorFromDimension from '../components/ReelLengthCalculatorFromDimension.vue'
import ReelLengthCalculatorFromWeight from '../components/ReelLengthCalculatorFromWeight.vue'
import ReelDiameterCalculatorFromLength from '../components/ReelDiameterCalculatorFromLength.vue'
import ReelWeightCalculatorFromDimension from '../components/ReelWeightCalculatorFromDimension.vue'
import ReelWeightCalculatorAfterDiameterReduction from '../components/ReelWeightCalculatorAfterDiameterReduction.vue'

export default {
  name: 'Home',
  components: {
    PalletWeightCalculator,
    ReelLengthCalculatorFromDimension,
    ReelLengthCalculatorFromWeight,
    ReelDiameterCalculatorFromLength,
    ReelWeightCalculatorFromDimension,
    ReelWeightCalculatorAfterDiameterReduction
  },
  data(){
    return{
      selectConversion: '0'
    }
  },
  methods:{
      changeSelection(evt){
        console.log(evt.target.value)
      }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 30px;
}
</style>
