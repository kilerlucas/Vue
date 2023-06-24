<template>
    <div role="dialog" aria-modal="true" class="fade modal show" tabindex="-1" style="display: block;">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <div class="modal-title h4">Ajouter un produit</div>
                    <button type="button" class="btn-close" aria-label="Close" @click="toggleProductModal"></button>
                </div>
                <div class="modal-body">
                    <form class="">
                        <input v-model="product.id" type="hidden">
                        <div>
                            <label class="form-label" for="productName">Nom</label>
                            <input v-model="product.name" required type="text" id="productName" class="form-control" >
                        </div>
                        <div>
                            <label class="form-label" for="productDescription">Description</label>
                            <textarea v-model="product.description" required rows="3" name="description" id="productDescription" class="form-control"></textarea>
                        </div>
                        <div>
                            <label class="form-label" for="productPrice">Prix</label>
                            <input v-model="product.price" required name="price" type="text" id="productPrice" class="form-control" >
                        </div>
                        <div>
                            <label class="form-label" for="productCategory">Catégorie</label>
                            <select v-model="product.type" required name="category" id="productCategory" class="form-control">
                                <option value="">Sélectionner une catégorie</option>
                                <option value="Food">Food</option>
                                <option value="Burguer">Burguer</option>
                                <option value="Italian">Italian</option>
                                <option value="Indian">Indian</option>
                                <option value="Thai">Thai</option>
                            </select>
                        </div>
                        <div>
                            <label class="form-label" for="productImage">Image</label>
                            <input v-model="product.photo" required id="productImage" class="form-control">
                        </div>
                        <button type="button" class="btn btn-primary mt-4" @click="saveProduct(product)">Ajouter</button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: ['inventory', 'toggleDeleteModal', 'toggleProductModal', 'saveProduct', 'curProduct'],
  data () {
    return {
      product: {
        id: '',
        name: '',
        photo: '',
        price: '',
        description: '',
        type: ''
      }
    }
  },
  methods: {
    newProduct () {
      this.submitted = false
      this.product = {}
    }
  }
}
</script>
