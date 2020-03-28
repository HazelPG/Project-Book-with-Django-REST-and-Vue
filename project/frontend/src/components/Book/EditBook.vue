<template lang="html">
    <div class="container">
        <div class="row">
            <div class="col tex-left">
                <h2>Editar Libro</h2>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <div class="card">
                    <div class="card-body">
                        <form @submit="onSubmit">
                            <div class="form-group row">
                                <label for="title" class="col-sm-2 col-form-label">Titulo: </label>
                                <div class="col-sm-6">
                                    <input type="text" placeholder="Titulo" name="title" class="form-control" v-model.trim="form.title">
                                </div>
                            </div>
                            <div class="form-group row">
                                <label for="description" class="col-sm-2 col-form-label">Descripción: </label>
                                <div class="col-sm-6">
                                    <textarea name="description" class="form-control" placeholder="Descripcion" rows="3" v-model.trim="form.description"></textarea>
                                </div>
                            </div>
                            <div class= "rows">
                                <div class="col tex-left">
                                    <b-button type="submit" variant="primary">
                                        Editar
                                    </b-button>
                                    <b-button type="submit" class="btn-large-space" :to="{name: 'ListBook'}">
                                        Cancelar
                                    </b-button>
                                </div>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>  
</template>

<script>
import axios from 'axios';
import swal from 'sweetalert';

export default {
    data () {
        return {
            bookId: this.$route.params.bookId,
            form: {
                title: '',
                description: ''
            }
        }
    }, 
    methods: {
        onSubmit (evt) {
            evt.preventDefault()

            const path =  `http://localhost:8000/api/v1.0/books/${this.bookId}/ `

            axios.put(path, this.form).then((respose) => {
                this.form.title = respose.data.title
                this.form.description = respose.data.description
                swal("Libro actualizado exitosamente!", "", "success")

            })
            .catch((error) => {
                console.log(error)
            })
        }, 

        getBooks (){
            const path =  `http://localhost:8000/api/v1.0/books/${this.bookId}/ `

            axios.get(path).then((respose) => {
                this.form.title = respose.data.title
                this.form.description = respose.data.description
            })
            .catch((error) => {
                console.log(error)
            })
        }
    },
    created () {
        this.getBooks()
    }
    
}
</script>

<style lang="css" scoped>

</style>