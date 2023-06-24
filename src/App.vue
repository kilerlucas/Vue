<template>
  <!-- Navigation-->
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container">
      <RouterLink class="navbar-brand" aria-current="page" to="/">
        Les Trésors de la Terre Cuite
      </RouterLink>
      <div class="navbar-collapse collapse" id="basic-navbar-nav">
        <div class="me-auto navbar-nav">
          <RouterLink class="nav-link active" aria-current="page" to="/">Home</RouterLink>
          <RouterLink class="nav-link" to="/produits">Produits</RouterLink>
          <RouterLink class="nav-link" to="/apropos">À propos</RouterLink>
        </div>
        <div class="ms-auto navbar-nav"><a href="#" role="button" data-rr-ui-event-key="#" class="nav-link" tabindex="0">
            <svg stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 512 512" height="1em" width="1em"
              xmlns="http://www.w3.org/2000/svg">
              <path
                d="M505 442.7L405.3 343c-4.5-4.5-10.6-7-17-7H372c27.6-35.3 44-79.7 44-128C416 93.1 322.9 0 208 0S0 93.1 0 208s93.1 208 208 208c48.3 0 92.7-16.4 128-44v16.3c0 6.4 2.5 12.5 7 17l99.7 99.7c9.4 9.4 24.6 9.4 33.9 0l28.3-28.3c9.4-9.4 9.4-24.6.1-34zM208 336c-70.7 0-128-57.2-128-128 0-70.7 57.2-128 128-128 70.7 0 128 57.2 128 128 0 70.7-57.2 128-128 128z">
              </path>
            </svg>
          </a>
          <a href="#" role="button" data-rr-ui-event-key="#" class="nav-link" tabindex="0">
            <svg stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 448 512" height="1em" width="1em"
              xmlns="http://www.w3.org/2000/svg">
              <path
                d="M224 256c70.7 0 128-57.3 128-128S294.7 0 224 0 96 57.3 96 128s57.3 128 128 128zm89.6 32h-16.7c-22.2 10.2-46.9 16-72.9 16s-50.6-5.8-72.9-16h-16.7C60.2 288 0 348.2 0 422.4V464c0 26.5 21.5 48 48 48h352c26.5 0 48-21.5 48-48v-41.6c0-74.2-60.2-134.4-134.4-134.4z">
              </path>
            </svg>
          </a>
          <a href="#" role="button" data-rr-ui-event-key="#" class="nav-link" tabindex="0">
            <svg stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 576 512" height="1em" width="1em"
              xmlns="http://www.w3.org/2000/svg">
              <path
                d="M528.12 301.319l47.273-208C578.806 78.301 567.391 64 551.99 64H159.208l-9.166-44.81C147.758 8.021 137.93 0 126.529 0H24C10.745 0 0 10.745 0 24v16c0 13.255 10.745 24 24 24h69.883l70.248 343.435C147.325 417.1 136 435.222 136 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-15.674-6.447-29.835-16.824-40h209.647C430.447 426.165 424 440.326 424 456c0 30.928 25.072 56 56 56s56-25.072 56-56c0-22.172-12.888-41.332-31.579-50.405l5.517-24.276c3.413-15.018-8.002-29.319-23.403-29.319H218.117l-6.545-32h293.145c11.206 0 20.92-7.754 23.403-18.681z">
              </path>
            </svg>
          </a>
        </div>
      </div>
    </div>
  </nav>
  <RouterView :inventory="inventory" :toggleDeleteModal="toggleDeleteModal" :toggleProductModal="toggleProductModal" />
  <DeleteModal v-if="showDeleteModal" :toggleDeleteModal="toggleDeleteModal" :product="curProduct"
    :confirmDelete="deleteProduct" />
  <!-- Product Modal -->
  <div v-if="showProductModal" role="dialog" aria-modal="true" class="fade modal show" tabindex="-1" style="display: block;">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <div class="modal-title h4">Ajouter un produit</div>
          <button type="button" class="btn-close" aria-label="Close" @click="toggleProductModal"></button>
        </div>
        <div class="modal-body">
          <form class="">
            <input v-model="curProduct.id" type="hidden">
            <div>
              <label class="form-label" for="productName">Nom</label>
              <input v-model="curProduct.name" required type="text" id="productName" class="form-control">
            </div>
            <div>
              <label class="form-label" for="productDescription">Description</label>
              <textarea v-model="curProduct.description" required rows="3" name="description" id="productDescription"
                class="form-control"></textarea>
            </div>
            <div>
              <label class="form-label" for="productPrice">Prix</label>
              <input v-model.number="curProduct.price" required name="price" type="text" id="productPrice" class="form-control">
            </div>
            <div>
              <label class="form-label" for="productCategory">Catégorie</label>
              <select v-model="curProduct.type" required name="category" id="productCategory" class="form-control">
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
              <input v-model="curProduct.photo" required id="productImage" class="form-control">
            </div>
            <button v-if="curProduct.id" type="button" class="btn btn-warning mt-4" @click="saveProduct(product)">Modifier</button>
            <button v-else type="button" class="btn btn-primary mt-4" @click="saveProduct(product)">Ajouter</button>
          </form>
        </div>
      </div>
    </div>
  </div>
  <!-- Footer-->
  <div class="mt-4 mb-4 container">
    <div class="text-center">
      <h3>Suivez-nous</h3>
      <div>
        <a href="https://www.facebook.com/"><svg stroke="currentColor" fill="currentColor" stroke-width="0"
            viewBox="0 0 512 512" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg">
            <path
              d="M504 256C504 119 393 8 256 8S8 119 8 256c0 123.78 90.69 226.38 209.25 245V327.69h-63V256h63v-54.64c0-62.15 37-96.48 93.67-96.48 27.14 0 55.52 4.84 55.52 4.84v61h-31.28c-30.8 0-40.41 19.12-40.41 38.73V256h68.78l-11 71.69h-57.78V501C413.31 482.38 504 379.78 504 256z">
            </path>
          </svg></a>
        <a href="https://www.pinterest.com/"><svg stroke="currentColor" fill="currentColor" stroke-width="0"
            viewBox="0 0 496 512" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg">
            <path
              d="M496 256c0 137-111 248-248 248-25.6 0-50.2-3.9-73.4-11.1 10.1-16.5 25.2-43.5 30.8-65 3-11.6 15.4-59 15.4-59 8.1 15.4 31.7 28.5 56.8 28.5 74.8 0 128.7-68.8 128.7-154.3 0-81.9-66.9-143.2-152.9-143.2-107 0-163.9 71.8-163.9 150.1 0 36.4 19.4 81.7 50.3 96.1 4.7 2.2 7.2 1.2 8.3-3.3.8-3.4 5-20.3 6.9-28.1.6-2.5.3-4.7-1.7-7.1-10.1-12.5-18.3-35.3-18.3-56.6 0-54.7 41.4-107.6 112-107.6 60.9 0 103.6 41.5 103.6 100.9 0 67.1-33.9 113.6-78 113.6-24.3 0-42.6-20.1-36.7-44.8 7-29.5 20.5-61.3 20.5-82.6 0-19-10.2-34.9-31.4-34.9-24.9 0-44.9 25.7-44.9 60.2 0 22 7.4 36.8 7.4 36.8s-24.5 103.8-29 123.2c-5 21.4-3 51.6-.9 71.2C65.4 450.9 0 361.1 0 256 0 119 111 8 248 8s248 111 248 248z">
            </path>
          </svg></a>
        <a href="https://www.instagram.com/"><svg stroke="currentColor" fill="currentColor" stroke-width="0"
            viewBox="0 0 448 512" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg">
            <path
              d="M224.1 141c-63.6 0-114.9 51.3-114.9 114.9s51.3 114.9 114.9 114.9S339 319.5 339 255.9 287.7 141 224.1 141zm0 189.6c-41.1 0-74.7-33.5-74.7-74.7s33.5-74.7 74.7-74.7 74.7 33.5 74.7 74.7-33.6 74.7-74.7 74.7zm146.4-194.3c0 14.9-12 26.8-26.8 26.8-14.9 0-26.8-12-26.8-26.8s12-26.8 26.8-26.8 26.8 12 26.8 26.8zm76.1 27.2c-1.7-35.9-9.9-67.7-36.2-93.9-26.2-26.2-58-34.4-93.9-36.2-37-2.1-147.9-2.1-184.9 0-35.8 1.7-67.6 9.9-93.9 36.1s-34.4 58-36.2 93.9c-2.1 37-2.1 147.9 0 184.9 1.7 35.9 9.9 67.7 36.2 93.9s58 34.4 93.9 36.2c37 2.1 147.9 2.1 184.9 0 35.9-1.7 67.7-9.9 93.9-36.2 26.2-26.2 34.4-58 36.2-93.9 2.1-37 2.1-147.8 0-184.8zM398.8 388c-7.8 19.6-22.9 34.7-42.6 42.6-29.5 11.7-99.5 9-132.1 9s-102.7 2.6-132.1-9c-19.6-7.8-34.7-22.9-42.6-42.6-11.7-29.5-9-99.5-9-132.1s-2.6-102.7 9-132.1c7.8-19.6 22.9-34.7 42.6-42.6 29.5-11.7 99.5-9 132.1-9s102.7-2.6 132.1 9c19.6 7.8 34.7 22.9 42.6 42.6 11.7 29.5 9 99.5 9 132.1s2.7 102.7-9 132.1z">
            </path>
          </svg></a>
      </div>
    </div>
  </div>
</template>

<script>
import DeleteModal from '@/components/DeleteModal.vue'
import ProductDataService from '@/services/ProductDataService'
export default {
  components: {
    DeleteModal
  },
  data () {
    return {
      showProductModal: false,
      showDeleteModal: false,
      inventory: [],
      curProduct: {
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
    toggleDeleteModal (id) {
      if (!isNaN(id)) {
        const prod = this.inventory.find((val) => val.id === id)
        this.curProduct.id = prod.id
        this.curProduct.name = prod.name
        this.curProduct.photo = prod.photo
        this.curProduct.price = prod.price
        this.curProduct.description = prod.description
        this.curProduct.type = prod.type
      } else {
        this.curProduct = {
          id: '',
          name: '',
          photo: '',
          price: '',
          description: '',
          type: ''
        }
      }
      this.showDeleteModal = !this.showDeleteModal
    },
    toggleProductModal (id) {
      if (!isNaN(id)) {
        const prod = this.inventory.find((val) => val.id === id)
        this.curProduct.id = prod.id
        this.curProduct.name = prod.name
        this.curProduct.photo = prod.photo
        this.curProduct.price = prod.price
        this.curProduct.description = prod.description
        this.curProduct.type = prod.type
      } else {
        this.curProduct = {
          id: '',
          name: '',
          photo: '',
          price: '',
          description: '',
          type: ''
        }
      }
      this.showProductModal = !this.showProductModal
    },
    addInventory (data) {
      this.inventory.push(data)
    },
    removeInventory (id) {
      this.inventory = this.inventory.filter((product) => {
        return product.id !== id
      })
    },
    updateInventory (id, data) {
      const prod = this.inventory.find((val) => val.id === id)

      prod.name = data.name
      prod.photo = data.photo
      prod.price = data.price
      prod.description = data.description
      prod.type = data.type
    },
    deleteProduct (id) {
      ProductDataService.delete(id)
        .then(response => {
          this.removeInventory(id)
          this.toggleDeleteModal()
        })
    },
    saveProduct () {
      if (this.curProduct.id) {
        ProductDataService.update(this.curProduct.id, this.curProduct)
          .then(response => {
            this.updateInventory(this.curProduct.id, this.curProduct)
            this.showProductModal = false
          })
      } else {
        delete this.curProduct.id
        ProductDataService.create(this.curProduct)
          .then(response => {
            this.curProduct.id = response.data.id
            this.addInventory(this.curProduct)
            this.showProductModal = false
          })
      }
    }
  },
  mounted () {
    ProductDataService.getAll()
      .then(response => {
        this.inventory = response.data
      })
  }
}
</script>
