<template>
    <div class="burger-table">
        <table>
            <thead>
                <th id="order-id">#</th>
                <th>Cliente</th>
                <th>Pão</th>
                <th>Carne</th>
                <th>Opcionais</th>
                <th>Ações</th>
            </thead>
            <tbody>
                <tr v-for="burger in burgers" :key="burger.id">
                    <td>{{burger.id}}</td>
                    <td>{{burger.nome}}</td>
                    <td>{{burger.carne}}</td>
                    <td>{{burger.pao}}</td>
                    <td>
                        <ul>
                            <li v-for="opcional in burger.opcionais" :key="opcional.index">
                                {{opcional}}
                            </li>
                        </ul>
                    </td>
                    <td>
                        <div class="action">
                            <select>
                                <option v-for="s in status" :key="s.id" :value="s.tipo"
                                :selected="burger.status == s.tipo">
                                    {{s.tipo}}
                                </option>
                            </select>
                            <button class="delete-btn" @click="deletarPedido(burger.id)">Excluir</button>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>


<script>
export default {
    name: 'Dashboard',

    data(){
        return {
            burgers: null,
            burger_id: null,
            status: [],
        }
    },

    methods: {
        async getPedidos() {
            const req = await fetch("http://localhost:3000/burgers")

            const data = await req.json()

            this.burgers = data
        },

        async getStatus() {
            const req = await fetch("http://localhost:3000/status")

            const data = await req.json()

            this.status = Array.from(data)
        },

        async deletarPedido(id){
            //ALGO ESPECIFICO DO JSON-SERVER 
            const req = await fetch(`http://localhost:3000/burgers/${id}`,{
                method: "DELETE"
            });

            const res = await req.json()

            this.getPedidos()

            //msg
        },

        async updateBurger(event, id) {
            //pega o status (valor) do select que o usuário colocou
            const option = event.target.value

            const dataJson = JSON.stringify({status:option})

            const req = await fetch(`http://localhost:3000/burgers/${id}`,{
                method: "PATCH",
                headers: {"Content-Type":"application/json"},
                body: dataJson
            })

            const res = await req.json()

            console.log(res)
        }
    },

    mounted(){

        //pega todos os pedidos
        this.getPedidos()

        //pega todos os status
        this.getStatus()
    }
    
}
</script>

<style scoped>
    table {
        margin: 0px auto;
    }

    table > thead > th {
        min-width: 200px;
        padding: 10px;
        border: 2px solid #111
    }

    table > tbody > tr > td {
        padding: 10px;
        border: 1px solid #111;
    }

    ul>li {
        list-style: none;
    }

    select {
        padding: 12px 6px;
        margin-right: 12px;
    }

    .delete-btn {
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        margin: 0 auto;
        transition: .5s;
        cursor: pointer;
    }

    .delete-btn:hover{
        background-color: transparent;
        color: #222;
    }

</style>