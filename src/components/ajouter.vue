<script setup lang="ts">
</script>
<template>
    <section>
    <div>
        <form class="form-floating" method="POST" action="" @click.prevent>
        
            <div class="modal-body">
                <label class="p-2">nom</label>
                <input type="text" class="form-control" name="nom" id="nom" v-model="nom" placeholder="nom">
        
                <label class="p-2">prenom</label>
                <input type="text" class="form-control" name="prenom" id="prenom" placeholder="prenom" v-model="prenom">
                <label class="p-2">email</label>
                <input type="email" class="form-control" name="email" id="email" placeholder="email" v-model="email">
                <br>
        
                <div class="modal-footer m-2">
                    <button type="reset" class="btn btn-danger" data-bs-dismiss="modal">Annuler</button>
                    <button type="submit" @click="add()" class="btn btn-success" id="submit">Ajouter</button>
                </div>
            </div>
        
        </form>
    </div>
    </section>
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
            window.location.href = "/"
        }

    }
};
</script>
