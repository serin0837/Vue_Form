<template>
    <div><!-- <form @submit.prevent="handleSubmit"> -->
    <!-- current -->
    <div class="form">
    <div>
        <span class="category">Visa</span>
        <label> Current Volume:</label>
        <input type="string"  v-model="visaCurrentVolume" @blur="calculate">
        <label> Current Rate:</label>
        <input type="number" step="0.01" v-model="visaCurrentRate" @blur="calculate"><span>%</span>
        <label> TP Rate:</label>
        <input type="number" step="0.01" v-model="visaTPRate"  @blur="calculate"><span>%</span>
        <p> Current Commission: {{visaCurrentCommission}} </p>
        <p> TP Commission:{{visaTPCommission}}</p>
        <p> Monthly Saving: {{visaMonthlySaving}} </p>
        <p> Annual Saving:{{visaAnnualSaving}}</p> 
    </div>

    <div>
        <span class="category">Mastercard</span>
        <label> Current Volume:</label>
        <input type="number" v-model="masterCurrentVolume" @blur="calculate">
        <label> Current Rate:</label>
        <input type="number" step="0.01" v-model="masterCurrentRate" @blur="calculate">
        <label> TP Rate:</label>
        <input type="number" step="0.01" v-model="masterTPRate" @blur="calculate">
        <p> Current Commission:{{masterCurrentCommission}}</p>
        <p> TP Commission:{{masterTPCommission}}</p> 
        <p> Monthly Saving: {{masterMonthlySaving}} </p>
        <p> Annual Saving:{{masterAnnualSaving}}</p> 
    </div>
    
    <div>
        <span class="category">Business</span>
        <label> Current Volume:</label>
        <input type="number"  v-model="businessCurrentVolume">
        <label> Current Rate:</label>
        <input type="number" step="0.01" v-model="businessCurrentRate">
        <label> TP Rate:</label>
        <input type="number" step="0.01"  v-model="businessTPRate">
        <p> Current Commission:{{businessCurrentCommission}}</p>
        <p> TP Commission:{{businessTPCommission}}</p> 
        <p> Monthly Saving: {{businessMonthlySaving}} </p>
        <p> Annual Saving:{{businessAnnualSaving}}</p> 
    </div>
    </div>
    <!-- <button>Calculate</button> -->
    <!-- </form> -->
    
    <!-- total saving debit -->
    <div class="total"> 
        <h5>Total Debit Saving</h5>
            <p>Monthly: {{totalDebitMonthlySaving}}</p>
            <p>Annual: {{totalDebitAnnualSaving}}</p>
    </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            visaCurrentVolume :'',
            visaCurrentRate :'',
            visaTPRate:'',
            masterCurrentVolume :'',
            masterCurrentRate :'',
            masterTPRate:'',
            businessCurrentVolume :'',
            businessCurrentRate :'',
            businessTPRate:'',

            visaCurrentCommission: '',
            visaTPCommission:'',
            masterCurrentCommission:'',
            masterTPCommission:'',
            businessCurrentCommission:'',
            businessTPCommission:'',

            visaMonthlySaving:'',
            visaAnnualSaving:'',
            masterMonthlySaving:'',
            masterAnnualSaving:'',
            businessMonthlySaving:'',
            businessAnnualSaving:'',

            totalDebitMonthlySaving:'',
            totalDebitAnnualSaving:''
        }
    },
    methods:{
        calculate(){
            this.visaCurrentCommission = Math.round((this.visaCurrentVolume * (this.visaCurrentRate*0.01))* 100)/100
            this.visaTPCommission = Math.round((this.visaCurrentVolume * (this.visaTPRate*0.01))*100)/100
            this.masterCurrentCommission = Math.round((this.masterCurrentVolume * (this.masterCurrentRate*0.01))*100)/100
            this.masterTPCommission = Math.round((this.masterCurrentVolume * (this.masterTPRate*0.01))*100)/100
            this.businessCurrentCommission = Math.round((this.businessCurrentVolume * (this.businessCurrentRate*0.01))*100)/100
            this.businessTPCommission = Math.round((this.businessCurrentVolume * (this.businessTPRate*0.01))*100)/100

            this.visaMonthlySaving = this.visaCurrentCommission - this.visaTPCommission
            this.visaAnnualSaving = this.visaMonthlySaving*12
            this.masterMonthlySaving = this.masterCurrentCommission - this.masterTPCommission
            this.masterAnnualSaving = this.masterMonthlySaving*12
            this.businessMonthlySaving = this.businessCurrentCommission - this.businessTPCommission
            this.businessAnnualSaving = this.businessMonthlySaving*12

            this.totalDebitMonthlySaving = this.visaMonthlySaving + this.masterMonthlySaving + this.businessMonthlySaving
            this.totalDebitAnnualSaving = this.visaAnnualSaving + this.masterAnnualSaving + this.businessAnnualSaving
    
        },
    }
}
</script>

<style scoped>
.form {
    max-width: 800px;
    margin: 30px auto;
    background:white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
  }
  label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
  }
  input {
    display: inline-block;
    padding: 10px 6px;
    width: 80px;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
  }
    .category{
        border-radius: 10px;
        padding:5px;
        background: rgb(71, 127, 249);
        margin:10px;
        width:20px;
    }
    p{
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    .total {
        max-width: 400px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px;
        border-radius: 10px;
    }
</style>