<template>
    <section>
    <div><h1>les utlisateurs:</h1>
        <div>
          <hr>
    
</div>
        <table border="1">
            <tr>
                <td>nom</td>
                <td>prenom</td>
                <td>email</td>
                <td><button type="button" class="btn btn-primary align-items-center pull-right m-2">
                    <a href="/ajouter" class="text-light"> Ajouter</a></button></td>
                <td></td>
            </tr>
            <tr v-for="todo of todos" v-bind:key="todo.id">
                <td>{{ todo.name }}</td>
                <td>{{ todo.prenom }}</td>
                <td>{{ todo.email }}</td>
                <td><button type="button" class="btn btn-success align-items-center">
                    <a v-bind:href=route+todo.id class="text-light">modifier</a>
                </button></td>
                <td><button type="submit" v-on:click="supp(todo.id)">
                        supp
                    </button></td>
    
            </tr>
        </table>
    
    </div></section>
</template>

<script>
import axios from "axios";

const baseURL = "http://localhost:3001/liste";

export default {
    name: "Liste",
    data() {
        return {
            todos: [],
            name: "",
            prenom: "",
            email: "",
         route: "/modifier/"
        };
    },
    async created() {
        try {
            const res = await axios.get(baseURL);

            this.todos = res.data;
        } catch (e) {
            console.error(e);
        }

    },
    methods: {
        async supp(id) {
            //    let resp= await axios.get('http://localhost:3000/user/1');
            //    console.log(resp.data);
            axios.delete('http://localhost:3001/liste/' + id);
            const res = await axios.get(baseURL);

            this.todos = res.data;
            
            window.location.href = "/"

        },
        






        async add() {
            try {
                const res = await axios.post(baseURL, { name: this.nom, prenom: this.prenom, email: this.email });


                this.todos = [...this.todos, res.data];

                this.name = "";
                this.prenom = "";
                this.email = "";
            } catch (e) {
                console.error(e);
            }
        },
        

    }
};
</script>

