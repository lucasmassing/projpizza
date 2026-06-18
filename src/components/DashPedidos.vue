<template>
    <div id="pizza-table" class="content-card">
        <div>
            <div id ="pizza-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Massa:</div>
                <div>Sabor:</div>
                <div>Opcionais:</div>
                <div>Ações:</div>
            </div>

        </div>
        <div id="pizza-table-rows">
            <div class="pizza-table-row" v-for="(pizza, index) in pizzasVisualizadas" :key="pizza.id">
                <div class="order-number">{{ index + 1 }}</div>
                <div>{{ pizza.nome }}</div>
                <div>{{ pizza.massa }}</div>
                <div>{{ pizza.sabor }}</div>
                <div>
                    <ul v-for="(opcional, index) in pizza.opcionais" :key="index">
                        <li>{{ opcional }}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updatePizza($event, pizza.id)">
                        <option :value="s.tipo" v-for="s in status" :key="s.id"
                                :selected="pizza.status == s.tipo">
                            {{ s.tipo }}
                        </option>
                    </select>
                    <button class="delete-btn" @click="deletePizza(pizza.id)">Cancelar</button>
                </div>
            </div>

        </div>

    </div>

</template>

<script>
export default {
    name:"DashPedidos",
    data(){
        return{
            pizzas: null,
            pizza_id: null,
            status:[],
            msg: null
        }
    },
    computed: {
        pizzasVisualizadas() {
            if (!Array.isArray(this.pizzas)) {
                return [];
            }

            return this.pizzas.map((pizza) => ({
                ...pizza
            }));
        }
    },
    methods:{
        async getPedidos(){
            const req = await fetch('http://localhost:3000/pizzas')

            const data = await req.json()

            this.pizzas = data

            this.getStatus()
        },
        async getStatus(){
            const req = await fetch('http://localhost:3000/status')

            const data = await req.json()

            this.status = data

        },
        async updatePizza(event, id){
            const option = event.target.value;


            const dataJson = JSON.stringify({status:option});

            const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
                method:"PATCH",
                headers:{"Content-Type":"application/json"},
                body:dataJson
            });

        },
        async deletePizza(id){
            const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
                method:"DELETE"
            });

            //tratar mensagem de exclusão

            this.getPedidos();
        }
    },
    mounted(){
        this.getPedidos()
    }
}



</script>

<style scoped>

    #pizza-table {
        max-width: 1200px;
        margin: 0 auto;
        padding: 10px;
        overflow: hidden;
        border-radius: var(--radius-lg);
    }

    #pizza-table-heading,
    #pizza-table-rows,
    .pizza-table-row {
        display: flex;
        flex-wrap: wrap;
    }

    #pizza-table-heading {
        font-weight: bold;
        padding: 18px 16px;
        border-bottom: 1px solid var(--line);
        background: linear-gradient(180deg, #fffaf4, #fff);
        color: var(--text);
        letter-spacing: 0.02em;
    }

    .pizza-table-row {
        width: 100%;
        padding: 18px 16px;
        border-bottom: 1px solid var(--line);
        background: rgba(255, 255, 255, 0.9);
        transition: transform .15s ease, background-color .15s ease;
    }

    .pizza-table-row:hover {
        background: #fffdf8;
        transform: translateY(-1px);
    }

    #pizza-table-heading div,
    .pizza-table-row div {
        width: 18%;
        padding-right: 10px;
        color: var(--text);
    }

    #pizza-table-heading .order-id,
    .pizza-table-row .order-number {
        width: 6%;
        font-weight: 800;
        color: var(--brand-dark);
    }

    .pizza-table-row ul {
        list-style: none;
        padding-left: 0;
        display: grid;
        gap: 6px;
    }

    .pizza-table-row li {
        display: inline-flex;
        align-items: center;
        padding: 8px 12px;
        border-radius: 999px;
        background: var(--surface-soft);
        border: 1px solid var(--line);
        color: var(--muted);
        width: fit-content;
    }

    select.status {
        width: min(100%, 190px);
        padding: 12px 14px;
        margin: 0 0 12px;
        border-radius: 14px;
        border: 1px solid var(--line);
        background: #fff;
        color: var(--text);
    }

    .delete-btn {
        background: linear-gradient(135deg, #222, #3a2a1d);
        color: #f4c15f;
        font-weight: bold;
        border: none;
        border-radius: 14px;
        padding: 12px 16px;
        font-size: 0.98rem;
        margin: 0;
        cursor: pointer;
        transition: transform .2s ease, opacity .2s ease, box-shadow .2s ease;
        box-shadow: 0 10px 18px rgba(34, 34, 34, 0.16);
    }
    
    .delete-btn:hover {
        transform: translateY(-1px);
        opacity: 0.96;
    }

    @media (max-width: 980px) {
        #pizza-table-heading div,
        .pizza-table-row div {
            width: 33.333%;
            margin-bottom: 10px;
        }

        #pizza-table-heading .order-id,
        .pizza-table-row .order-number {
            width: 12%;
        }
    }

    @media (max-width: 680px) {
        #pizza-table-heading,
        .pizza-table-row {
            padding: 16px 12px;
        }

        #pizza-table-heading div,
        .pizza-table-row div {
            width: 100%;
            padding-right: 0;
        }

        #pizza-table-heading .order-id,
        .pizza-table-row .order-number {
            width: 100%;
        }
    }
  
</style>
