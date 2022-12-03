<template>
    <div class="row">
        <div class="card" id="total">
            <h2>Total de pedidos</h2>
            <span>{{ valorPedidos }}</span>
        </div>

        <div class="card" id="pendentes">
            <h2>Pedidos pendentes</h2>
            <span>{{ valorPendentes }}</span>
        </div>

        <div class="card" id="concluidos">
            <h2>Pedidos concluídos</h2>
            <span>{{ valorConcluidos }}</span>
        </div>
    </div>
</template>

<script>
export default {
    name: "Painel",
    props: {
        valorPedidos: Number,
        valorPendentes: Number,
        valorConcluidos: Number
    }
}
</script>

<style scoped>
    .row {
        display: flex;
        justify-content: center;
        align-items: center ;
        flex-wrap: wrap;
        font-family: "Poppins", sans-serif;
    }
    .card {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-around;
        border-radius: 5px;
        box-shadow: 7px 7px 13px 0px rgba(50, 50, 50, 0.22);
        padding: 30px;
        margin: 20px;
        width: 300px;
        height: 150px;
    }
    .card h2,
    .card span {
        text-align: center;
        font-weight: bold;
    }
    .card h2 {
        font-size: 1.3em;
    }
    
    .card span {
        font-size: 2em;
        
    }


    #total {
        border-left: 4px solid #4895ff;
    }
    
    #concluidos {
    border-left: 4px solid #3bb54a;
    }
    
    #pendentes {
    border-left: 4px solid #b3404a;
    }

    @media only screen and (max-width: 1120px) {
        .card {
            width: 200px;
        }
    }

    @media only screen and (max-width: 820px) {
        .card {
            width: 150px;
        }
    }

</style>