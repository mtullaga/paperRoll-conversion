<template>
  <div>
    <div class="col-md-12" style="margin-top: 20px">
        <b-row class="justify-content-md-center">
            <b-col class="boxShadow" cols="6" style="border: 1px solid grey; border-radius: 10px; padding: 10px">
              <h5 style="text-align: center">Reel Diameter Calculator From Length</h5>
              <p>
                <i style="color: grey">Enter Values to calculate result.All Fields are mandatory.</i>
              </p>
              <table >
                  <tr>
                    <td>Meterage:</td>
                    <td><input type="number" v-model="ReelCalculatorMeterage" style="margin-bottom: 7px;"></td>
                    <td>m</td>
                  </tr>
                  <tr>
                    <td>Caliper:</td>
                    <td><input type="number" v-model="ReelCalculatorCaliper" style="margin-bottom: 7px;"></td>
                    <td>mic</td>
                  </tr>
                  <tr>
                    <td>Core Diameter (inside):</td>
                    <td><input type="number" v-model="ReelCalculatorCore" style="margin-bottom: 7px;"></td>
                    <td>mm</td>
                  </tr>

                  <tr>
                    <td>Core Wall Thickness:</td>
                    <td><input type="number" v-model="ReelCalculatorCoreWall" style="margin-bottom: 7px;"></td>
                    <td>mm</td>
                  </tr>

                  <tr>
                    <td><b>Diameter: </b></td>
                    <td><input type="text" v-model="ReelCalculatorDiameter" id="result" style="font-weight: bold;" readonly></td>
                    <td>mm</td>
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
                      <button class="btn btn-success" @click="ReelCalculator" style="margin-top: 0px"><b>CALCULATE</b></button>
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
    name: 'ReelDiameterCalculatorFromLength',
    data() {
      return {
            ReelCalculatorMeterage: null,
            ReelCalculatorCaliper: null,
            ReelCalculatorCore: null,
            ReelCalculatorCoreWall: null,
            ReelCalculatorDiameter: null,

      }
    },
    methods:{
      ReelCalculator(){

            var area, radius, diameter;
            var Meterage = this.ReelCalculatorMeterage 
            var Caliper = this.ReelCalculatorCaliper 
            var Core = this.ReelCalculatorCore 
            var CoreWallThickness = this.ReelCalculatorCoreWall


            radius = (parseFloat(Core / 2) + parseFloat(CoreWallThickness));
            area = (Caliper * Meterage + (Math.PI * Math.pow(radius,2))) / Math.PI;
            diameter = Math.sqrt(area) * 2;

            this.ReelCalculatorDiameter = parseFloat(Math.round(diameter).toFixed(2));

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
            this.ReelCalculatorMeterage = null
            this.ReelCalculatorCaliper = null
            this.ReelCalculatorCore = null
            this.ReelCalculatorCoreWall = null
            this.ReelCalculatorDiameter = null
        
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