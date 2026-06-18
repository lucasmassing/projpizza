<template>  

    <div>
        <Message :msg="msg" v-show="msg"/>
        <div>
            <form id="pizza-form" method="POST" @submit="criarpizza">
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
            const req = await fetch('http://localhost:3000/ingredientes');
            const data = await req.json();

            this.massas = data.massas
            this.sabores = data.sabores
            this.opcionaisdata = data.opcionais
        },
        async criarpizza(e){
            e.preventDefault();
            const data = {
                nome: this.nome,
                massa: this.massa,
                sabor: this.sabor,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            }
            console.log(data)
            const dataJson =JSON.stringify(data);
            const req = await fetch("http://localhost:3000/pizzas", {
                method:"POST",
                headers:{"Content-Type":"application/json"},
                body:dataJson
            });

            const res = await req.json()
            console.log(res)

            this.msg = `Pedido nº ${res.id} realizado com sucesso!`

            setTimeout(()=> this.msg = "", 3000)

            //limpar
            this.nome=""
            this.massa=""
            this.sabor=""
            this.opcionais=[]
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
   
</style>
