<template>
    <div class="wrapper">
            <div class="container-flex">
                <div class="form">
                <div>
                    <input type="text" name="product" id="product" placeholder="Insert product">
                </div>
                <div>
                    <input type="text" name="brand" id="brand" placeholder="Insert brand">
                </div>
                <div>
                    <input type="text" name="market" id="market" placeholder="Insert market name">
                </div>
                <div>
                    <input type="number" name="qty" id="qty" placeholder="Insert quantity">
                </div>
                <button @click="addList()">add to list</button>
                <button @click="saveItems()">save list</button>
            </div>
        </div>
        <div class="wishlist">
            <div class="card" v-for="(item, n) in items" :key="item.product">
                <div class="card-title">
                    <p>{{item.product}}</p>
                </div>
                <div class="card-brand">
                    <p>{{item.brand}}</p>
                </div>
                <div class="card-mkt-name">
                    <span>{{item.market}}</span>
                </div>
                <div class="card-qty">
                    <p>{{item.qty}}</p>
                </div>
                <div class="close">
                    <button id="edit-card" @click="editItems(n)">Edit</button>
                    <button id="close-card" @click="removeItems(n)">Delete</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'FormItens',
        data() {
            return {
                items: []
            }
        },
        mounted() {
            if (localStorage.getItem('items')) {
                try {
                    this.items = JSON.parse(localStorage.getItem('items'))
                } catch (error) {
                    this.localStorage.removeItem('items')
                }
            }
        },
        methods: {
            addList() {
                let product = document.getElementById('product');
                let qty = document.getElementById('qty');
                let brand = document.getElementById('brand');
                let market = document.getElementById('market');
                this.items.push({
                    product: product.value,
                    qty: qty.value,
                    market: market.value,
                    brand: brand.value
                })
            },
            removeItems(x) {
                this.items.splice(x, 1)
                this.saveItems()
            },
            saveItems() {
                const parsed = JSON.stringify(this.items)
                localStorage.setItem('items', parsed)
            },
            editItems() {
                
            }
        },
    }
</script>

<style lang="css">
    .container-flex {
        display: flex;
        justify-content: center;

    }

    .container-flex div {
        text-align: center;
    }

    .form {
        width: 400px;
        display: flex;
        justify-content: center;
        flex-direction: column;
        justify-content: center;
        box-shadow: 0 0 20px #ccc;
        padding: 20px;
    }

    .wishlist {
        display: flex;
        flex-direction: column;
        justify-content: center;
        padding: 50px;
    }

    input {
        border: 1px solid #424242;
        border-radius: 5px;
        width: 100%;
        height: 35px;
        margin-top: 15px;
    }

    p {
        font-size: 1.3em;
    }

    button {
        border-radius: 5px;
        font-family: Arial, Helvetica, sans-serif;
        border: none;
        color: #fff;
        font-size: 14px;
        height: 45px;
        width: 100%;
        background-color: #bc4749;
        margin-top: 12px;
        cursor: pointer;
    }

    button:hover {
        background-color:#cf7475;
    }

    .card {
        width: 100%;
        background-color: rgb(255, 255, 255);
        box-shadow: 0 0 20px rgb(134, 134, 134);
        display: flex;
        justify-content: space-around;
        align-items: center;
        text-align: center;
        border-radius: 10px;
        margin: 5px;
    }

    .card div {
        width: 25%;
    }

    .card div p {
        font-size: 14px;
    }
    .card-mkt-name span {
        background-color: #6a994e;
        padding: 2px 10px;
        color: #fff;
        font-weight: 400;
        font-size: 14px;
        border-radius: 3px;
    }
    #close-card {
        width: 85px;
        height: 35px;
        margin: 7px;
        background-color: #6a994e;
    }
    #edit-card {
        width: 85px;
        height: 35px;
        margin: 7px;
        background-color: #a7c957;
    }
</style>