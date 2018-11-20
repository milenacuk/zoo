<template>
<div>
    <h2>Add animals</h2>
    <form @submit.prevent="addAnimal" class="form-horizontal">
        <label>Sort</label>
        <input v-model="newAnimal.sort" placeholder="Enter sort">
        <label>Name</label>
        <input v-model="newAnimal.name" placeholder="Enter name">
        <label>Date</label>
        <input v-model="newAnimal.date" placeholder="Enter date"><br>
        <label>Sector</label>


   <select v-model="newAnimal.sector" class='form-control'>
       <!-- <option></option> -->
        <option v-for="(sector,index) in sectors" :key='index' v-bind:value="sector">
            {{ sector.surface }}            
        </option> 
    </select><br>
    


        <button>Add animal</button>     
        
    </form>

    <h2>Animals</h2>
    <center>
    <table border=1>
        <thead>
            <tr>
                <th>Key</th>
                <th>Sort</th>
                <th>Name</th>
                <th>Date</th>  
                <th>Sector</th>              
            </tr>
        </thead>
        <tbody>
            <tr v-for="(animal,index) in animals" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ animal.sort }}</td>
                <td>{{ animal.name }}</td>
                <td> {{!animal.date ? 'nepoznat' : animal.date}}</td> 
                <td>{{ animal.sector.name }}</td>
                <td> <button @click="removeAnimal(animal)">Delete</button></td>    
                <td><button @click="onTop(animal)">Move to top</button></td>       
            </tr>
        </tbody>
     
    </table>
    </center>
    <h2>Sectors</h2>
        <center>
            <table border=1>
                <thead>
                    <tr>
                        <th>Key</th>
                        <th>Sector</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(sector,index) in sectors" :key="index">
                        <td>{{ index + 1 }}</td>
                        <td>{{ sector.name }}</td>
                        <td> <button @click="showAnimals(sector)">Show</button></td>  
                    </tr>
                </tbody>
            </table>
        </center>
</div>
</template>

<script>
const sectors = [
    { name: 'Water-animal', surface: 'Water'},
    { name: 'Fawl', surface: 'Kages'},
    { name: 'Predators', surface: 'Kages'}
    
]
export default {
    data(){
        return{
            animals: [
                { sort: "konj", name: "Keti" , date: '', sector: sectors[0] },
                { sort: "konj", name: "Keti" , date: '', sector: sectors[0] },
                { sort: "pas", name: "Dzoni" , date: '1-1-2018', sector: sectors[1] },
                { sort: "majmun", name: "Klempo" ,date: '22-7-2016', sector: sectors[2] },
                { sort: "macka", name: "Kiki" , date: '15-3-2010', sector: sectors[2] },
                { sort: "kit", name: "Loki" , date: '6-9-2012', sector: sectors[1] },
                { sort: "pas", name: "Bea" , date: '12-11-2017', sector: sectors[0] }
                
            ],
            newAnimal: {
            sort: '',
            name: '',
            date: '',
            sector: {}
        },
        sectors: sectors  
        // ovde sam stavila tu konstantu u objekat
        }
        
    },
    methods: {
        removeAnimal(animal){
            let index = this.animals.indexOf(animal);
            this.animals.splice(index,1);
        },
        onTop(animal){
            
            this.removeAnimal(animal);
            this.animals.unshift(animal);
        },
        addAnimal(){
            // if(this.animal.sector )
            this.animals.push(this.newAnimal);
            this.newAnimal = {};
        },
        showAnimals(sector){
            var animalsToShow = [];
           this.animals.forEach(function(animal){
               if(animal.sector.name === sector.name){
                   animalsToShow.push(animal.name);
               }
           });
           alert(animalsToShow);
        }

    }
}
</script>
