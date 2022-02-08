<template>
    <div class="flex items-center justify-center bg-sky-300 h-screen">
        <div class="w-80 h-96 bg-slate-300 shadow-lg shadow-sky-600/50 rounded-md">
            
            <!-- hasil kalkulasi -->
            <div class=" w-11/12 h-10 rounded-md px-5 mx-auto my-3 text-right bg-slate-50 ">
               <p class=" py-1 font-semibold text-lg"> {{ calculatorValue || 0 }}</p>
            </div>

            <!-- tombol-tombol -->
            <div class="grid gap-y-3 grid-cols-4 items-center justify-items-center px-3 ">
            <button class="border border-blue-400 w-16 h-12 rounded-md" v-for="n in calculatorElements" :key="n" :class="{'bg-emerald-500 border-emerald-500':['C','*','/','-','+','%','='].includes(n)}" @click="action(n)">
                {{n}}
            </button>
            </div>

        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            calculatorValue: '',
            calculatorElements: ['C','*','/','-','7','8','9','+','4','5','6','%','1','2','3','=','0','.'],
        }
    },

    methods: {
        action(n){
            if(!isNaN(n) || n === '.'){
                this.calculatorValue += n + '';
            }
        
            if(n === 'C'){
                this.calculatorValue = ''; 
            }

            if(n === '%'){
                this.calculatorValue = this.calculatorValue / 100 + '';
            }

            if(['*','/','-','+'].includes(n)){
                this.operator = n;
                this.previousCalculatorValue = this.calculatorValue;
                this.calculatorValue = '';
            }

            if(n === '='){
                this.calculatorValue = eval(
                    this.previousCalculatorValue + this.operator + this.calculatorValue
                );

                this.previousCalculatorValue = '';
                this.operator = null;
            }
        
        }
    }
}
</script>