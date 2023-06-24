<template>
    <!-- Section-->
    <section class="py-5">
        <div class="container px-4 px-lg-5 mt-5">
            <button type="button" class="btn btn-primary mb-5" @click="toggleProductModal">Ajouter un produit</button>
            <div class="row gx-4 gx-lg-5 row-cols-2 row-cols-md-3 row-cols-xl-4 justify-content-center">
                <div v-for="(product, i) in inventory" :key="i" class="col-4 mb-5">
                    <!-- Product image-->
                    <img alt="{{ product.name }}" className="img-fluid"
                        :src="require(`@/assets/img/450/${product.photo}`)" />
                    <!-- Product details-->
                    <div className="box-content">
                        <h4>{{ product.name }}</h4>
                        <p>{{ product.description }}</p>
                        <p>Prix: {{ product.price.toFixed(2) }}</p>
                        <p>Catégorie: {{ product.type }}</p>
                        <p>Description: {{ product.description }}</p>

                        <div class="card-body p-4">
                            <div class="text-center">
                                <!-- Product name-->
                                <RouterLink :to="{ name: 'product', params: { id: product.name } }">
                                    <h5 class="fw-bolder">View {{ product.name }}</h5>
                                </RouterLink>
                            </div>
                        </div>
                        <!-- Product actions-->
                        <Button variant="dark" className="btn btn-dark mr-2" @click="toggleProductModal(product.id)">
                            Modifier
                        </Button>
                        <Button class="btn btn-danger m-2" @click="toggleDeleteModal(product.id)">
                            Supprimer
                        </Button>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
export default {
  props: ['inventory', 'toggleDeleteModal', 'toggleProductModal']
}
</script>
