<template>
    <div class="row product-container">
        <app-product v-for="product in productList" >
            <img class="card-img-top" :src='product.selectedImage' :alt='product.title'>
        <div class="card-body">
          <h5 class="card-title">{{ product.title }}</h5>
          <small>
            <strong>Adet : </strong>{{product.count}}
          </small>
          <br>
          <small>
            <strong>Fiyat : </strong> {{ product.price }}
          </small>
          <br>
          <small>
            <strong>Tutar : </strong> {{ product.totalPrice }}
          </small>
        </div>
        </app-product>
    
    </div>
</template>

<script>
    import {eventBus} from "../main";
    import Product from "./Product";
    export default {
        components:{
            appProduct : Product
        },
        data(){
            return {
                productList: [],
            }
        },
        created(){
            //event ladığım bir durumu on metodu ile dinliyorum
            eventBus.$on("productAdded", (product) =>{
                this.productList.push(product);
                eventBus.$emit("progressBarUpdated", this.productList.lenght);

            });
         }
    }
</script>

<style scoped>

</style>