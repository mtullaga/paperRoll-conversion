<template>
  <div>
    <div class="col-md-12" style="margin-top: 20px">
        <b-row class="justify-content-md-center">
            <b-col class="boxShadow" cols="6" style="border: 1px solid grey; border-radius: 10px; padding: 10px">
              <h5 style="text-align: center">Reel Length Calculator From Weight</h5>
              <p>
                <i style="color: grey">Enter Values to calculate result.All Fields are mandatory.</i>
              </p>
              <table >
                  <tr>
                    <td>Net Weight:</td>
                    <td><input type="number" v-model="ReelLenCalcWeightWt" style="margin-bottom: 7px;"> kg</td>
                  </tr>
                  <tr>
                    <td>Width:</td>
                    <td><input type="number" v-model="ReelLenCalcWeightWidth" style="margin-bottom: 7px;"> mm</td>
                  </tr>
                  <tr>
                    <td>Substance:</td>
                    <td><input type="number" v-model="ReelLenCalcWeightSubstance" style="margin-bottom: 7px;"> gsm</td>
                  </tr>

                  <tr>
                    <td><b>Linear Metres</b></td>
                    <td><input type="text" v-model="ReelLenCalcWeightLinearM" id="result" style="font-weight: bold;" readonly> metres</td>
                  </tr>
                  <tr>
                    <td colspan="2" style="font-size: 12px">
                        *Use 10 mm as a default.<br>
                        For more specific info please consult your Metsä Board contact.
                    </td>
                  </tr>
                  <tr>
                    <td></td>
                    <td>
                      <button class="btn btn-success" @click="ReelLenCalcWeight" style="margin-top: 0px"><b>CALCULATE</b></button>
                      <button class="btn btn-danger" @click="clear" style="margin: 0px 0px 0px 10px"><b>Clear</b></button>
                    
                    </td>
                  </tr>
              </table>

              </b-col>
          </b-row>
      </div>
  </div>
</template>

<script>
  export default {
    name: 'ReelLengthCalculatorFromWeight',
    data() {
      return {
            ReelLenCalcWeightWt: null,
            ReelLenCalcWeightWidth: null,
            ReelLenCalcWeightSubstance: null,
            ReelLenCalcWeightLinearM: null,

      }
    },
    methods:{
      ReelLenCalcWeight(){

            var LinearMeter
            var Weight = this.ReelLenCalcWeightWt 
            var Width = this.ReelLenCalcWeightWidth 
            var Substance = this.ReelLenCalcWeightSubstance

            LinearMeter = ((Weight * 1000 * 1000) / (Substance * Width));

            this.ReelLenCalcWeightLinearM = parseFloat(Math.round(LinearMeter).toFixed(2));

            setTimeout(()=>{
              let testingCodeToCopy = document.querySelector('#result')
              testingCodeToCopy.setAttribute('type', 'text') 
              testingCodeToCopy.select()

              try {
                var successful = document.execCommand('copy');
                var msg = successful ? 'successful' : 'unsuccessful';
                alert('Weight of board ' + msg + ' copied to clipboard.');
              } catch (err) {
                alert('Oops, unable to copy');
              }
            }, 200)
          
      },

      clear(){
            this.ReelLenCalcWeightWt = null
            this.ReelLenCalcWeightWidth = null
            this.ReelLenCalcWeightSubstance = null
            this.ReelLenCalcWeightLinearM = null
        
      }
    }
  }
</script>

<style scoped>
  .boxShadow{
    -webkit-box-shadow: 0 10px 6px -6px #777;
    -moz-box-shadow: 0 10px 6px -6px #777;
          box-shadow: 0 10px 6px -6px #777;

  }
</style>