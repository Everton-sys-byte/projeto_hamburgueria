<template>
    <div>
        <p>alert</p>
        <form class="burger-form" @submit.prevent="createBurger()">
            <div class="input-container">
                <label for="nome">Nome do cliente:</label>
                <input type="text" ref="nome" v-model="nome" placeholder="Digite o seu nome">
            </div>
            <div class="input-container">
                <label for="pao">Escolha o pão:</label>
                <select v-model="pao">
                    <option value="">Selecione seu pão</option>
                    <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{pao.tipo}}</option>
                </select>
            </div>
            <div class="input-container">
                <label for="carne">Escolha a carne:</label>
                <select v-model="carne">
                    <option value="">Selecione o tipo de carne</option>
                    <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
                </select>
            </div>
            <div class="opcionais-container input-container">
                <label for="opcionais" class="opcionais-title">Selecione os opcionais:</label>
                <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                    <input type="checkbox" v-model="opcionais" :value="opcional.tipo">
                    <span>{{opcional.tipo}}</span>
                </div>
            </div>
            <div class="input-container">
                <input type="submit" class="submit-btn" value="Criar meu Burger">
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: 'BurgerForm',

    data() {
        return {
            msg: null,

            //variaveis relacionadas ao formulario
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],

            //variaveis relacionadas a API interna que esta no diretório DB na raiz do projeto
            paes: null,
            carnes: null,
            opcionaisdata: null,
        }
    },

    methods: {
        async getIngredientes(){

            //consome a api
            const req = await fetch("http://localhost:3000/ingredientes")

            //coloca a resposta da api dentro de data
            const data = await req.json()

            //inserindo os valores da resposta de forma dinâmica nas variáveis que estão no return de data()
            this.paes = data.paes
            this.carnes = data.carnes
            this.opcionaisdata = data.opcionais
        },

        async createBurger(){
            //console.log('teste')
            //criando um objeto data
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "solicitado"
            }

            //transformando o objeto data(JSON) para string
            const dataJson = JSON.stringify(data)

            //enviando as informações para a API 
            const req = await fetch("http://localhost:3000/burgers",{
                method: "POST",
                headers: {
                    "Content-type" : "application/json"
                },
                body: dataJson
            })

            const res = await req.json()

            //limpando os campos
            this.nome = ""
            this.carne = ""
            this.pao = ""
            this.opcionais = []

            //colocando o focus utilizando o ref do vue (o ref está no input type nome)
            this.$refs.nome.focus()
        }
    },

    //LifeCycleHooks (quando o componente for montado)
    mounted() {
        this.getIngredientes()
    }

}
</script>

<style scoped>

    .burger-form {
        max-width: 400px;
        margin: 0 auto;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 20px;
    }

    .input-container label{
        font-weight: bold;
        margin-bottom: 15px;
        color: #222;
        padding: 5px 10px;
        border-left: 4px solid #FCBA03;
    }

    .input-container input, select {
        padding: 5px 10px;
        width: 300px;
    }

    .opcionais-container {
        flex-direction: row;
        flex-wrap: wrap;
    }

    .opcionais-title {
        width: 100%;
    }

    .checkbox-container {
        display: flex;
        align-items: start;
        width: 50%;
        margin-bottom: 20px;
    }

    .checkbox-container span, 
    .checkbox-container input {
        width: auto;
    }

    .checkbox-container span {
        margin-left: 6px;
        font-weight: bold;
    }

    .submit-btn {
        background: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 16px;
        cursor: pointer;
        transition: .5s;
    }

    .submit-btn:hover {
        background: transparent;
        color: #222;
    }
</style>