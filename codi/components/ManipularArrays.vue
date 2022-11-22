<template>
    <v-container>
        <v-row>
            <v-col cols="12"  md="6" >
                <v-text-field
                    label="Temperatura"
                    placeholder="Escriu la temperatura"
                    type="number"
                    v-model="temperatura"
                ></v-text-field>
                <v-btn @click="afegir()">afegir</v-btn>
                <v-btn @dblclick="netejar()">netejar</v-btn>
                <v-btn @mouseenter="borrarDarrerElement()">Borrar darrer</v-btn>
                <v-btn @click="temperaturesAleatories()">Aleatori</v-btn>

            </v-col>
            <v-col cols="12" md="6" >
                Resultat:
                <br>
                Mostres: {{tamanyArray}}
                <br>
                Mostres superiors a 50 graus: {{mesDe50}}
                <br>
                
                <v-sparkline
                    :value="temperatures"
                    :gradient="elMeuArrayDeColors"
                 
                ></v-sparkline>
                <div v-for="element in temperatures">
                    La temperatura és {{element}}
                </div>
            </v-col>
        </v-row>
    </v-container>
</template>
<script>
  
    export default{
       mounted(){
            // Inicialitzem l'array de temperatures
            this.temperaturesAleatories()
            
       },
       data(){
            return{
                elMeuArrayDeColors:['red', 'blue','yellow'],
                temperatura:0,
                temperatures:[],
            }
       },
       methods:{
            afegir(){
                console.log("Afegint...")
                console.log("temperatura:",this.temperatura)
                console.log("El tipus de temperatura és",typeof(this.temperatura))
                const tmp = parseFloat(this.temperatura)
                console.log("El tipus de temperatura és",typeof(tmp))
                this.temperatures.push(tmp)
            },
            netejar(){
                console.log("netejant..")
                this.temperatures = []
                console.log(this.temperatures)
            },
            borrarDarrerElement(){
                console.log("borrant últim element..")
                this.temperatures.pop()
            },
            temperaturesAleatories(){
                console.log("fent temperatures aleatories")

                // Creem un array buid 
                var nouArray = []
                // repetim 100 vegades
                for(var i = 0;i<100;i++){
                    // afegim valors
                    var valorAleatoriDecimals = Math.random()*100
                    var valorAleatoriEnter = this.processarEnter(valorAleatoriDecimals)
                    nouArray.push(valorAleatoriEnter)
                }
                // Assignem al array del component
                this.temperatures = nouArray


            },
            processarEnter(val){
                return parseInt(val)
            }
       },
       computed:{
            tamanyArray(){
                return this.temperatures.length
            },
            mesDe50(){
                var mostresDeMesDe50Graus = 0
                this.temperatures.forEach((temperatura)=>{
                    if(temperatura>50){
                        mostresDeMesDe50Graus++
                    }
                })
                return mostresDeMesDe50Graus
            },
       },
       watch:{
        temperatura(newValue,oldValue){
            console.log(newValue,oldValue)
        },
        mesDe50(newValue,oldValue){
            if(newValue>55){
                alert("ALERTA")
            }
        }
       }

    }
</script>