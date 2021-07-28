<template>
  <div>
    <div class="col-md-12" style="margin-top: 20px">
        <b-row class="justify-content-md-center">
            <b-col class="boxShadow" cols="6" style="border: 1px solid grey; border-radius: 10px; padding: 10px">
              <h5 style="text-align: center">Reel Weight Calculator From Dimension</h5>
              <p>
                <i style="color: grey">Enter Values to calculate result.All Fields are mandatory.</i>
              </p>
              <table >
                  <tr>
                    <td>Substance:</td>
                    <td><input type="number" v-model="ReelWtCalcDimentionSubstance" style="margin-bottom: 7px;"> gsm</td>
                  </tr>
                  <tr>
                    <td>Caliper:</td>
                    <td><input type="number" v-model="ReelWtCalcDimentionCaliper" style="margin-bottom: 7px;"> mic</td>
                  </tr>
                  <tr>
                    <td>Width:</td>
                    <td><input type="number" v-model="ReelWtCalcDimentionWidth" style="margin-bottom: 7px;"> mm</td>
                  </tr>
                  <tr>
                    <td>Overall Diameter:</td>
                    <td><input type="number" v-model="ReelWtCalcDimentionODiameter" style="margin-bottom: 7px;"> mm</td>
                  </tr>
                  <tr>
                    <td>Core Diameter (inside):</td>
                    <td><input type="number" v-model="ReelWtCalcDimentionCDiameter" style="margin-bottom: 7px;"> mm</td>
                  </tr>
                  <tr>
                    <td>Core Wall thickness:</td>
                    <td><input type="number" v-model="ReelWtCalcDimentionCthick" style="margin-bottom: 7px;"> mm</td>
                  </tr>
                  <tr>
                    <td><b>Net Weight</b></td>
                    <td><input type="text" v-model="ReelWtCalcDimentionWeight" id="result" style="font-weight: bold;" readonly> kg</td>
                  </tr>
                  <tr>
                    <td colspan="2" style="font-size: 12px">
                        1Weight of Board only - no bungs, cores, etc.<br>
                        *Use 10 mm as a default.<br>
                        For more specific info please consult your Metsä Board contact.
                    </td>
                  </tr>
                  <tr>
                    <td></td>
                    <td>
                      <button class="btn btn-success" @click="ReelWtCalcDimention" style="margin-top: 0px"><b>CALCULATE</b></button>
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
    name: 'ReelWeightCalculatorFromDimension',
    data() {
      return {
          ReelWtCalcDimentionCaliper: null,
          ReelWtCalcDimentionSubstance: null,
          ReelWtCalcDimentionWidth: null,
          ReelWtCalcDimentionODiameter: null,
          ReelWtCalcDimentionCDiameter: null,
          ReelWtCalcDimentionCthick: null,
          ReelWtCalcDimentionWeight: null
      }
    },
    methods:{
      ReelWtCalcDimention(){

            var Substance = this.ReelWtCalcDimentionSubstance
            var Caliper =  this.ReelWtCalcDimentionCaliper
            var Width = this.ReelWtCalcDimentionWidth
            var OverallDiameter = this.ReelWtCalcDimentionODiameter
            var CoreDiameter = this.ReelWtCalcDimentionCDiameter
            var CoreWallThickness = this.ReelWtCalcDimentionCthick
            
            var Weightkg ,Materialdensitygm;

            Materialdensitygm = Substance / Caliper;

            Weightkg = ((Math.pow((OverallDiameter / 2), 2)) - (Math.pow(((CoreDiameter / 2) + parseFloat(CoreWallThickness)), 2))) * Math.PI * Width * (Materialdensitygm / Math.pow(10,6));
            
            this.ReelWtCalcDimentionWeight = parseFloat(Math.round(Weightkg).toFixed(2));

            setTimeout(()=>{
              let testingCodeToCopy = document.querySelector('#result')
              testingCodeToCopy.setAttribute('type', 'text') 
              testingCodeToCopy.select()

              try {
                var successful = document.execCommand('copy');
                var msg = successful ? 'successful' : 'unsuccessful';
                alert('Net Weight ' + msg + ' copied to clipboard.');
              } catch (err) {
                alert('Oops, unable to copy');
              }
            }, 200)
          
      },

      clear(){
          this.ReelWtCalcDimentionSubstance =  null
          this.ReelWtCalcDimentionCaliper =  null
          this.ReelWtCalcDimentionWidth =  null
          this.ReelWtCalcDimentionODiameter =  null
          this.ReelWtCalcDimentionCDiameter =  null
          this.ReelWtCalcDimentionCthick =  null
          this.ReelWtCalcDimentionWeight =  null
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