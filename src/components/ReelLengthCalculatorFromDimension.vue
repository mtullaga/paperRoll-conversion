<template>
  <div>
    <div class="col-md-12" style="margin-top: 20px">
        <b-row class="justify-content-md-center">
            <b-col class="boxShadow" cols="6" style="border: 1px solid grey; border-radius: 10px; padding: 10px">
              <h5 style="text-align: center">Reel Length Calculator From Dimension</h5>
              <p>
                <i style="color: grey">Enter Values to calculate result.All Fields are mandatory.</i>
              </p>
              <table >
                  <tr>
                    <td>Caliper:</td>
                    <td><input type="number" v-model="ReelLengthDimCalliper" style="margin-bottom: 7px;"></td>
                    <td>mic</td>
                  </tr>
                  <tr>
                    <td>Overall Diameter:</td>
                    <td><input type="number" v-model="ReelLengthDimOverallDiameter" style="margin-bottom: 7px;"></td>
                    <td>mm</td>
                  </tr>
                  <tr>
                    <td>Core Diameter (inside):</td>
                    <td><input type="number" v-model="ReelLengthDimCoreDiameter" style="margin-bottom: 7px;"></td>
                    <td>mm</td>
                  </tr>
                  <tr>
                    <td>Core Wall Thickness: </td>
                    <td><input type="number" v-model="ReelLengthDimCoreThickness" style="margin-bottom: 7px;"></td>
                    <td>mm</td>
                  </tr>
                  
                  <tr>
                    <td><b>Linear Metres</b></td>
                    <td><input type="text" v-model="ReelLengthDimLinearMetres" id="result" style="font-weight: bold;" readonly></td>
                    <td>metres</td>
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
                      <button class="btn btn-success" @click="ReelLenCalcDiamention" style="margin-top: 0px"><b>CALCULATE</b></button>
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
    name: 'ReelLengthCalculatorFromDimension',
    data() {
      return {
            ReelLengthDimCalliper: null,
            ReelLengthDimOverallDiameter: null,
            ReelLengthDimCoreDiameter: null,
            ReelLengthDimCoreThickness: null,
            ReelLengthDimLinearMetres: null,
      }
    },
    methods:{
      ReelLenCalcDiamention(){

            var Caliper = this.ReelLengthDimCalliper
            var OverallDiameter = this.ReelLengthDimOverallDiameter
            var CoreDiameter = this.ReelLengthDimCoreDiameter
            var CoreWallThickness=this.ReelLengthDimCoreThickness

 
            var x, Linearmm;
                            
            
            CoreWallThickness = CoreWallThickness*2;
            x=Math.pow((OverallDiameter/2000),2)-Math.pow(((parseFloat(CoreDiameter)+ parseFloat(CoreWallThickness))/2000),2);
                
                Linearmm=(x/Caliper)*Math.pow(10,6)* Math.PI;
                
            this.ReelLengthDimLinearMetres = parseFloat(Math.round(Linearmm).toFixed(2));

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
            this.ReelLengthDimCalliper = null
            this.ReelLengthDimOverallDiameter = null
            this.ReelLengthDimCoreDiameter = null
            this.ReelLengthDimCoreThickness = null
            this.ReelLengthDimLinearMetres = null
        
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