<template>
    <div>
        <div style="width:20px">
            <div>
                <label for="name">Name</label>
                <input type="text" v-model.lazy="table.inputName" placeholder="Enter your name here">
            </div>
            <div>
                <label for="work">Designation</label>
                <input type="text" v-model.lazy="table.inputWork" placeholder="Enter your Designation here">
            </div>
        </div>
        <div>
            <button class="save" @click="saveData">Save</button>
        </div>
        <div>
            <table >
                <thead>
                    <tr>
                        <th>Name</th>
                        <th>Designation</th>
                        <th>Edit</th>
                        <th>Delete</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="(data,index) in savedData" :key="index">
                        <td>{{ data.name }}</td>
                        <td>{{ data.work }}</td>
                        <td><button class="edit" @click="editData(index)">Edit</button></td>
                        <td> <button class="delete" @click="deleteData(index)">Delete</button></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    name: 'createCrud',
    data() {
        return {
            table: {
                inputName: '',  
                inputWork: '', 
            },
            savedData: [],
            editIndex :null,
        };
    },
    methods: {
        saveData() {
            if (this.table.inputName && this.table.inputWork) {
                if(this.editIndex != null){
                    this.savedData[this.editIndex].name = this.table.inputName;
                    this.savedData[this.editIndex].work = this.table.inputWork;
                    this.editIndex =null;
                    alert("your data is updated successfully")
                }
                else{
                this.savedData.push({
                    name: this.table.inputName,
                    work: this.table.inputWork
                });
                }
                
                alert("Your data has been saved successfully!");
                 this.table.inputName = '';
                 this.table.inputWork = ''; 
            }
           
            else {
                alert("Please fill in both Name and Designation before saving.");
            }
        },
        deleteData(index){
            this.savedData.splice(index,1);
        },
        editData(index){
            this.table.inputName = this.savedData[index].name;
            this.table.inputWork  = this.savedData[index].work;
            this.editIndex = index;
        },
    }
};
</script>

<style scoped>
table, td, th, tr {
    border: 1px solid black;
    border-collapse: collapse;
    padding: 8px;
    text-align: center;
    width: 60%;
    margin-top: 20px;
}

.save {
    margin-top: 10px;
  padding: 5px 10px;
    background-color: rgb(94, 145, 94);
    color: white;
    border: none;
    cursor: pointer;
   
}
.save:hover {
    background-color: rgb(74, 115, 74);
}
.delete {
    margin-top: 10px;
  padding: 5px 10px;
    background-color: rgb(226, 9, 34);
    color: white;
    border: none;
    cursor: pointer;
   
}
.delete:hover {
    background-color: rgb(160, 44, 63);
}
.edit {
    margin-top: 10px;
  padding: 5px 10px;
    background-color: rgba(55, 49, 49);
    color: white;
    border: none;
    cursor: pointer;
   
}
.edit:hover {
    background-color: rgb(139, 128, 130);
}
</style>
