<template>
    <Message :msg="msg" v-show="msg"/>
    <div id="burger-table">
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Ações</div>
            </div>
        </div>
        <div id="burger-table-rows">
            <div v-for:="burger in burgers" class="burger-table-row">
                <div class="order-number">{{ burger.id }}</div>
                <div>{{ burger.name }}</div>
                <div>{{ burger.bread }}</div>
                <div>{{ burger.meat }}</div>
                <div>
                    <ul>
                        <li v-for:="optional in burger.optional">{{ optional }}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updateBurger($event, burger.id)">
                        <option value="" disabled>Selecione</option>
                        <option :value="s.tipo" v-for:="s in status" :selected="burger.status == s.tipo">{{ s.tipo }}</option>
                    </select>
                    <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
    
</template>

<script>

import Message from './Message.vue'

export default {
    name: 'Dashboard',
    components: {
        Message
    },
    data() {
        return {
            burgers: null,
            burger_id: null,
            status: [],
            msg: null
        }
    },
    methods: {
        async getRequestBurger() {
            const req = await fetch('http://localhost:3000/burgers')
            const data = await req.json()
            
            this.burgers = data
            this.burger_id = data.id

            this.getStatus()
        },
        async getStatus() {
            const req = await fetch('http://localhost:3000/status')
            const data = await req.json()

            this.status = data

        },
        async deleteBurger(id) {


            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'DELETE'
            })

            const res = await req.json()

            this.msg = `Pedido Nº ${id} removido com sucesso!`

            setTimeout(() => this.msg = '', 3000)

            this.getRequestBurger()

        },
        async updateBurger(event, id) {

            const option = event.target.value

            const dataJson = JSON.stringify({status: option})

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: 'PATCH',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: dataJson
            })

            const data = await req.json()

            this.msg = `Pedido Nº ${id} definido como ${option}.`

            setTimeout(() => this.msg = '', 3000)
            


        }
    },
    mounted() {
        this.getRequestBurger()
    }
}
</script>

<style scoped>
    
    #burger-table {
        max-width: 1200px;
        margin: 0 auto;
    }

    #burger-table-heading,
    #burger-table-rows,
    .burger-table-row {
        display: flex;
    }

    #burger-table-rows {
        flex-wrap: wrap;
    }

    #burger-table-heading {
        font-weight: bold;
        padding: 0.75rem;
        border-bottom: 3px solid #333;
    }

    #burger-table-heading div,
    .burger-table-row div {
        width: 19%;
    }

    .burger-table-row {
        width: 100%;
        padding: 0.75rem;
        border-bottom: 1px solid #ccc;
    }

    #burger-table-heading .order-id,
    .burger-table-row .order-number {
        width: 5%;
    }

    select {
        padding: .75rem .375rem;
        margin-right: .75rem;
    }

    .delete-btn {
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        margin: 0 auto;
        font-size: 1rem;
        padding: .625rem;
        cursor: pointer;

        transition:  .3s;
    }

    .delete-btn:hover {
        background-color: transparent;
        color: #222;
        border: 1px solid #222;
    }

</style>