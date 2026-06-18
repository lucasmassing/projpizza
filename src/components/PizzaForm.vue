<template>  

    <div class="form-shell content-card">
        <Message :msg="msg" v-show="msg"/>
        <div>
            <form id="pizza-form" method="POST" @submit.prevent="criarpizza">
                <div class="input-container">
                    <label for="nome">Nome do cliente:</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
                </div>
                <div class="input-container">
                    <label for="massa">Escolha a massa:</label>
                    <select name="massa" id="massa" v-model="massa">
                      <option value="">Selecione a sua massa</option>
                      <option v-for="massa in massas" :key="massa.id" 
                      :value="massa.tipo">
                      {{ massa.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="sabor">Escolha o sabor da sua pizza:</label>
                    <select name="sabor" id="sabor" v-model="sabor">
                      <option value="">Selecione o sabor da pizza</option>
                      <option v-for="sabor in sabores" :key="sabor.id" 
                      :value="sabor.tipo">
                      {{ sabor.tipo }}</option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="opcionais">Selecione os opcionais:</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{opcional.tipo}}</span>
                    </div>
                </div>
                <div class="input-container">
                    <input class="submit-btn" type="submit" value="Criar minha pizza!">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from './Message'

export default {
    name:"PizzaForm",
    data(){
        return {
            massas: null,
            sabores: null,
            opcionaisdata: null,
            nome: null,
            massa: null,
            sabor: null,
            opcionais: [],
            msg: null
        }    
    },
    methods: {
        async getIngredientes() {
            try {
                const req = await fetch('http://localhost:3000/ingredientes');
                const data = await req.json();

                this.massas = data.massas
                this.sabores = data.sabores
                this.opcionaisdata = data.opcionais
            } catch (error) {
                this.msg = 'Não foi possível carregar os ingredientes. Inicie o backend com npm run backend.'
            }
        },
        async criarpizza(e){
            try {
                const data = {
                    nome: this.nome,
                    massa: this.massa,
                    sabor: this.sabor,
                    opcionais: Array.from(this.opcionais),
                    status: "Solicitado"
                }

                const dataJson = JSON.stringify(data);
                const req = await fetch("http://localhost:3000/pizzas", {
                    method:"POST",
                    headers:{"Content-Type":"application/json"},
                    body:dataJson
                });

                const res = await req.json()

                this.msg = `Pedido nº ${res.id} realizado com sucesso!`

                setTimeout(()=> this.msg = "", 3000)

                this.nome=""
                this.massa=""
                this.sabor=""
                this.opcionais=[]

                this.$router.push('/pedidos')
            } catch (error) {
                this.msg = 'Não foi possível criar a pizza. Verifique se o backend está ativo.'
            }
        }
    },
    mounted () {
        this.getIngredientes()
    },
    components:{
        Message
    }
}
</script>

<style scoped>
     .form-shell {
        max-width: 920px;
        margin: 0 auto;
        padding: 34px;
        border-radius: var(--radius-lg);
     }

     #pizza-form {
        display: grid;
        grid-template-columns: repeat(2, minmax(0, 1fr));
        gap: 22px 28px;
     }

     .input-container {
        display: flex;
        flex-direction: column;
        gap: 10px;
     }

     .input-container label {
        font-weight: 700;
        color: var(--text);
        font-size: 0.98rem;
     }

     .input-container input[type='text'],
     .input-container select {
        width: 100%;
        border: 1px solid var(--line);
        background: var(--surface-soft);
        color: var(--text);
        border-radius: var(--radius-md);
        padding: 16px 18px;
        font-size: 1rem;
        outline: none;
        transition: border-color .2s ease, box-shadow .2s ease, transform .2s ease;
     }

     .input-container input[type='text']:focus,
     .input-container select:focus {
        border-color: var(--brand);
        box-shadow: 0 0 0 4px rgba(217, 119, 6, 0.14);
        transform: translateY(-1px);
     }

     .input-container:nth-child(4) {
        grid-column: 1 / -1;
     }

     .checkbox-container {
        display: flex;
        align-items: center;
        gap: 10px;
        padding: 12px 14px;
        margin-bottom: 10px;
        background: #fff;
        border: 1px solid var(--line);
        border-radius: 14px;
     }

     .checkbox-container input {
        width: 18px;
        height: 18px;
        accent-color: var(--brand);
     }

     .checkbox-container span {
        color: var(--muted);
        font-weight: 600;
     }

     .input-container:last-child {
        grid-column: 1 / -1;
     }

     .submit-btn {
        border: none;
        border-radius: 999px;
        padding: 16px 24px;
        background: linear-gradient(135deg, var(--brand), #f59e0b);
        color: #fff;
        font-size: 1rem;
        font-weight: 800;
        letter-spacing: 0.02em;
        cursor: pointer;
        box-shadow: 0 14px 26px rgba(217, 119, 6, 0.28);
        transition: transform .2s ease, box-shadow .2s ease, filter .2s ease;
     }

     .submit-btn:hover {
        transform: translateY(-2px);
        box-shadow: 0 18px 30px rgba(217, 119, 6, 0.34);
        filter: brightness(1.02);
     }

     .submit-btn:active {
        transform: translateY(0);
     }

     @media (max-width: 820px) {
        .form-shell {
            padding: 22px;
        }

        #pizza-form {
            grid-template-columns: 1fr;
        }
     }
</style>
