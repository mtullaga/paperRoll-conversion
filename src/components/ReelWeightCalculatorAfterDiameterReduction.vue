<template>
  <div>
    <div class="col-md-12" style="margin-top: 20px">
        <b-row class="justify-content-md-center">
            <b-col class="boxShadow" cols="6" style="border: 1px solid grey; border-radius: 10px; padding: 10px">
              <h5 style="text-align: center">Reel Weight Calculator After Diameter Reduction</h5>
              <p>
                <i style="color: grey">Enter Values to calculate result.All Fields are mandatory.</i>
              </p>
              <table >
                  <tr>
                      <td><i>ORIGINAL REEL DETAILS</i></td>
                      <td></td>
                  </tr>
                  <tr>
                    <td>Net Weight:</td>
                    <td><input type="number" v-model="ReelWtCalcAfterDiameterWeight" style="margin-bottom: 7px;"> kg</td>
                  </tr>
                  <tr>
                    <td>Width:</td>
                    <td><input type="number" v-model="ReelWtCalcAfterDiameterWidth" style="margin-bottom: 7px;"> mm</td>
                  </tr>
                  <tr>
                    <td>Overall Diameter:</td>
                    <td><input type="number" v-model="ReelWtCalcAfterDiameterODiameter" style="margin-bottom: 7px;"> mm</td>
                  </tr>

                  <tr>
                    <td>Core Diameter (inside): </td>
                    <td><input type="number" v-model="ReelWtCalcAfterDiameterCDiameter" style="margin-bottom: 7px;"> mm</td>
                  </tr>
                 <tr>
                      <td><i>NEW REEL DETAILS</i></td>
                      <td></td>
                  </tr>
                  <tr>
                    <td>
                        Core Wall Thickness:
                    </td>
                    <td><input type="number" v-model="ReelWtCalcAfterDiameterDiameter" style="margin-bottom: 7px;"> mm</td>
                  </tr>

                  <tr>
                    <td><b>Diameter: </b></td>
                    <td><input type="text" v-model="ReelWtCalcAfterDiameterNWeight" id="result" style="font-weight: bold;" readonly> kg</td>
                  </tr>
                  <tr>
                    <td colspan="2" style="font-size: 12px">
                        Weight of Board only - no bungs, cores, etc.<br>
                       
                    </td>
                  </tr>
                  <tr>
                    <td></td>
                    <td>
                      <button class="btn btn-success" @click="ReelWtCalcAfterDiameter" style="margin-top: 0px"><b>CALCULATE</b></button>
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
    name: 'ReelWeightCalculatorAfterDiameterReduction',
    data() {
      return {
            ReelWtCalcAfterDiameterWeight: null,
            ReelWtCalcAfterDiameterWidth: null,
            ReelWtCalcAfterDiameterODiameter: null,
            ReelWtCalcAfterDiameterCDiameter: null,
            ReelWtCalcAfterDiameterDiameter: null,
            ReelWtCalcAfterDiameterNWeight: null,

      }
    },
    methods:{
      ReelWtCalcAfterDiameter(){

            var weight = this.ReelWtCalcAfterDiameterWeight 
            var Width = this.ReelWtCalcAfterDiameterWidth 
            var OverallDiameter = this.ReelWtCalcAfterDiameterODiameter
            var CoreDiameter=this.ReelWtCalcAfterDiameterCDiameter
            var Diameter=this.ReelWtCalcAfterDiameterDiameter

            var PIR,PIR1,MaterialDensity, NewWeight;
        
            var convunit1=10;

            OverallDiameter=OverallDiameter/convunit1;
            CoreDiameter=CoreDiameter/convunit1;
            Width=Width/convunit1;
            weight=weight*1000;
            Diameter=Diameter/convunit1;
            
            PIR=(Math.PI * (Math.pow((OverallDiameter/2),2))) - (Math.PI * (Math.pow((CoreDiameter/2),2)));
            
            MaterialDensity = (weight / (PIR * Width));

            PIR1=(Math.PI * (Math.pow((Diameter/2),2))) - (Math.PI * (Math.pow((CoreDiameter/2),2)));
            
            NewWeight = (PIR1 * MaterialDensity * Width);
            
            NewWeight=NewWeight/1000;
            
            // $("#ReelWtCalcAfterDiameterMatDen").val(parseFloat(MaterialDensity.toFixed(2)));
            this.ReelWtCalcAfterDiameterNWeight =parseFloat(Math.round(NewWeight).toFixed(2));

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
            this.ReelWtCalcAfterDiameterWeight = null
            this.ReelWtCalcAfterDiameterWidth = null
            this.ReelWtCalcAfterDiameterODiameter = null
            this.ReelWtCalcAfterDiameterCDiameter = null
            this.ReelWtCalcAfterDiameterDiameter = null
            this.ReelWtCalcAfterDiameterNWeight = null
        
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