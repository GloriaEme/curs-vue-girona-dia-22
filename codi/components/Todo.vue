<template>
    <v-container>
        <v-row>
            <v-col cols="12" sm="6">
                <v-textarea
                label="Tasca"
                placeholder="p.e: fer el llit" 
                outlined>
                </v-textarea>
                <v-btn text>afegir tasca</v-btn>
            </v-col>
            <v-col cols="12" sm="6">
                <v-row class="tasca" v-for="tasca in tasques">
                    <v-col cols="8">
                       <h2>{{tasca.text}}</h2>
                    </v-col>
                    <v-col cols="4">
                        <v-checkbox
                            v-model="tasca.feta"
                        ></v-checkbox>
                    </v-col>
                </v-row>
                <pre>
                    {{tasques}}
                </pre>
                
            </v-col>   
        </v-row> 
    </v-container>
</template>

<script>
export default{
    data(){
        return {       
            tasques:[
                {
                    text:"Fer el llit",
                    feta:true
                },
                {
                    text:"Fer els deures",
                    feta:false
                },
                {
                    text:"Anar a comprar",
                    feta:true
                }]
        }
    }
}
</script>


<style>
    .tasca{
        background-color: bisque;
        margin-bottom: 10px;
    }
</style>