<template>
<Message :msg="msg" v-show="msg"/>
    <div id="form">
        <form id="burger-form" @submit="createBurger($event)">
            <div class="input-container">
                <label for="name">Nome do cliente:</label>
                <input type="text" placeholder="Digite seu nome" id="name" name="name" v-model="name" required>
            </div>
            <div class="input-container">
                <label for="bread">Escolha o pão:</label>
                <select id="bread" name="bread" v-model="bread" required>
                    <option value="" disabled selected>Selecione o tipo de pão</option>
                    <option v-for:="bread in breads" :value="bread.tipo">
                        {{ bread.tipo }}
                    </option>
                </select>
            </div>
            <div class="input-container">
                <label for="meat">Escolha a carne:</label>
                <select id="meat" name="meat" v-model="meat" required>
                    <option value="" disabled selected>Selecione o tipo de carne</option>
                    <option v-for:="meat in meats" :value="meat.tipo">
                        {{ meat.tipo }}
                    </option>
                </select>
            </div>
            <div class="checkbox-container">
                <label for="">Selecione os opcionais:</label>
                <div class="checkbox" v-for:="option in optionalData">
                    <input type="checkbox" name="optional" id="" v-model="optional" :value="option.tipo">
                    <span>
                        {{ option.tipo }}
                    </span>
                </div>
            </div>
            <div class="button">
                <button type="submit">Criar meu Burger!</button>
            </div>
        </form>
    </div>
</template>

<script>

import Message from './Message.vue'

export default {
    name: 'Form',
    components: {
        Message
    },
    data() {
        return {
            breads: null,
            meats: null,
            optionalData: null,
            name: null,
            bread: null,
            meat: null,
            optional: [],
            msg: null

        }
    },
    methods: {
        async getIngredients() {
            const req = await fetch('http://localhost:3000/ingredientes')
            const data = await req.json()

            this.breads = data.paes
            this.meats = data.carnes
            this.optionalData = data.opcionais

        },
        async createBurger(event) {
            event.preventDefault()
            const data = {
                name: this.name,
                meat: this.meat,
                bread: this.bread,
                optional: Array.from(this.optional),
                status: 'Solicitado'
            }

            const dataJSON = JSON.stringify(data)
            
            const req = await fetch('http://localhost:3000/burgers', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: dataJSON
            })

            const res = await req.json()

            this.msg = `Pedido Nº ${res.id} realizado com sucesso`

            setTimeout(() => this.msg = '', 3000)

            this.name = ''
            this.meat = ''
            this.bread = ''
            this.optional = ''

        }
    },
    mounted() {
        this.getIngredients()
    }
}
</script>

<style scoped>
    #form {
        display: flex;
        justify-content: left;
        margin: 1rem auto;

        max-width: 550px;
    }

    .input-container label,
    .checkbox-container label {
        border-left: 4px solid #FCBA03;
        height: 2.2rem;
        display: flex;
        align-items: center;

        text-indent: 0.7rem;
        color: #222;
        font-size: 1.125rem;
        font-weight: bold;

        margin-bottom: 1.5rem;
    }

    .input-container input {
        text-indent: 0.7rem;
    }

    .input-container input,
    .input-container select {
        width: 100%;
        height: 2.5rem;
        border: 1px solid #333;
        border-radius: 2px;

        margin-bottom: 1.5rem;
    }

    .input-container input::placeholder {
        text-indent: 0.7rem;
        font-size: 1rem;
        color: rgb(160, 160, 160);
    }

    .checkbox-container {
        width: 270px;
        display: flex;
        flex-wrap: wrap;
        gap: 1rem;
    }

    .checkbox {
        display: flex;
        gap: .3rem;
        align-items: center;
    }

    .checkbox span {
        font-size: 1.125rem;
        font-weight: 600;
    }

    .button {
        width: 550px;
        display: flex;
        justify-content: center;
    }

    button {
        margin-top: 1.5rem;

        font-size: 1.2rem;
        font-family: Helvetica, sans-serif;
        color: #FCBA03;
        background-color: #111;
        border: none;
        padding: 0.5rem;
        width: 300px;

        cursor: pointer;

        transition: .3s;
    }

    button:hover {
        background-color: transparent;
        color: #222;
        border: 1px solid #222;
    }
</style>