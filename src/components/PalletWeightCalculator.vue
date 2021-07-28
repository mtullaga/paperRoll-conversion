<template>
  <div>
    <div class="col-md-12" style="margin-top: 20px">
        <b-row class="justify-content-md-center">
            <b-col class="boxShadow" cols="6" style="border: 1px solid grey; border-radius: 10px; padding: 10px">
              <h5 style="text-align: center">Pallet Weight Calculator</h5>
              <p>
                <i style="color: grey">Enter Values to calculate result.All Fields are mandatory.</i>
              </p>
              <table >
                  <tr>
                    <td>Number of Sheets:</td>
                    <td><input type="number" v-model="PalletNoSheet" style="margin-bottom: 7px;"></td>
                    <td>pcs</td>
                  </tr>
                  <tr>
                    <td>Sheet Width:</td>
                    <td><input type="number" v-model="PalletWidth" style="margin-bottom: 7px;"></td>
                    <td>mm</td>
                  </tr>
                  <tr>
                    <td>Sheet Length:</td>
                    <td><input type="number" v-model="PalletLength" style="margin-bottom: 7px;"></td>
                    <td>mm</td>
                  </tr>
                  <tr>
                    <td>Substance: </td>
                    <td><input type="number" v-model="PalletSubstance" style="margin-bottom: 7px;"></td>
                    <td>gsm</td>
                  </tr>
                  
                  <tr>
                    <td><b>Weight of Board on Pallet</b></td>
                    <td><input type="text" v-model="PalletWtBoard" id="result" style="font-weight: bold;" readonly></td>
                    <td>kg</td>
                  </tr>
                  
                  <tr>
                    <td></td>
                    <td>
                      <button class="btn btn-success" @click="PalletWeightCalc" style="margin-top: 10px"><b>CALCULATE</b></button>
                      <button class="btn btn-danger" @click="clear" style="margin: 10px 0px 0px 10px"><b>Clear</b></button>
                    
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
          PalletNoSheet: null,
          PalletWidth: null,
          PalletLength: null,
          PalletSubstance: null,
          PalletWtBoard: null,
      }
    },
    methods:{
      PalletWeightCalc(){

            var NoOfSheet = this.PalletNoSheet
            var SheetWidth = this.PalletWidth
            var SheetLength = this.PalletLength
            var Substance = this.PalletSubstance

            var area, PalletWt;

            area=((SheetWidth * SheetLength) / 1000000);
            PalletWt = ((area * Substance * NoOfSheet) / 1000);
          
            this.PalletWtBoard = Math.round(PalletWt);

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
          this.PalletNoSheet =  null
          this.PalletWidth =  null
          this.PalletLength =  null
          this.PalletSubstance =  null
          this.PalletWtBoard =  null
        
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