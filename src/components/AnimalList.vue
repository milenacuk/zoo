<template>
<div>
    <h2>Add animals</h2>
    <form @submit.prevent="addAnimal">
        <label>Sort</label>
        <input v-model="newAnimal.sort" placeholder="Enter sort">
        <label>Name</label>
        <input v-model="newAnimal.name" placeholder="Enter name">
        <label>Date</label>
        <input v-model="newAnimal.date" placeholder="Enter date">
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
            </tr>
        </thead>
        <tbody>
            <tr v-for="(animal,index) in animals" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ animal.sort }}</td>
                <td>{{ animal.name }}</td>
                <td> {{!animal.date ? 'nepoznat' : animal.date}}</td>    
                <td> <button @click="removeAnimal(animal)">Delete</button></td>    
                <td><button @click="onTop(animal)">Move to top</button></td>       
            </tr>
        </tbody>
    </table>
    </center>
</div>
</template>

<script>
export default {
    data(){
        return{
            animals: [
                { sort: "konj", name: "Keti" , date: '' },
                { sort: "konj", name: "Keti" , date: '' },
                { sort: "pas", name: "Dzoni" , date: '1-1-2018' },
                { sort: "majmun", name: "Klempo" ,date: '22-7-2016' },
                { sort: "macka", name: "Kiki" , date: '15-3-2010' },
                { sort: "kit", name: "Loki" , date: '6-9-2012' },
                { sort: "pas", name: "Bea" , date: '12-11-2017' }
                
            ],
            newAnimal: {
            sort: '',
            name: '',
            date: ''
        }
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
            this.animals.push(this.newAnimal);
            this.newAnimal = {};
        }

    }
}
</script>
