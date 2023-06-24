<template>
    <div role="dialog" aria-modal="true" class="fade modal show" style="display: block;">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <div class="modal-title h4">Supprimer un produit</div>
                    <button type="button" class="btn-close" aria-label="Close" @click="toggleDeleteModal"></button>
                </div>
                <div class="modal-body">
                    <p>Êtes-vous sûr de vouloir supprimer le produit "{{ product?.name }}" ?</p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" @click="toggleDeleteModal">Annuler</button>
                    <button type="button" class="btn btn-danger" @click="confirmDelete(product.id)">Supprimer</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  props: ['toggleDeleteModal', 'product', 'confirmDelete']
}
</script>
