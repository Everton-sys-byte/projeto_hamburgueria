<template>
    <div>
        <p>alert</p>
        <form class="burger-form">
            <div class="input-container">
                <label for="nome">Nome do cliente:</label>
                <input type="text" name="nome" id="nome" class="nome" v-model="nome" placeholder="Digite o seu nome">
            </div>
            <div class="input-container">
                <label for="pao">Escolha o pão:</label>
                <select name="pao" id="pao" class="pao" v-model="pao">
                    <option value="">Selecione seu pão</option>
                    <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{pao.tipo}}</option>
                </select>
            </div>
            <div class="input-container">
                <label for="carne">Escolha a carne:</label>
                <select name="carne" id="carne" class="carne" v-model="pao">
                    <option value="">Selecione o tipo de carne</option>
                    <option value="maminha">Maminha</option>
                </select>
            </div>
            <div class="opcionais-container input-container">
                <label for="opcionais" class="opcionais-title">Selecione os opcionais:</label>
                <div class="checkbox-container">
                    <input type="checkbox" name="opcionais" id="" v-model="opcionais" value="salame">
                    <span>Salame</span>
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
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            status: 'solicitado',
            msg: null,
        }
    },

    methods: {
        async getIngredientes(){
            const req = await fetch("http://localhost:3000/ingredientes")
            const data = await req.json()

            console.log(data)

            this.paes = data.paes
            this.carnes = data.carnes
            this.opcionaisdata = data.opcionais
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