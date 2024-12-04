<template>
    <div class="col-hp">
        <div class="card h-100 shadow-sm">
            <figure>
                <img v-bind:src="product.get_thumbnail" class="card-img-top" >
            </figure>

                <div class="card-body">
                    <div class="clearfix mb-3">
                        <span class="float-start badge rounded-pill bg-success">₦{{ product.price}}</span>

                    </div>
                    <h5 class="card-title">
                        <router-link v-bind:to="product.get_absolute_url" >{{ product.name }}</router-link>
                    </h5>

                    <div class="d-grid gap-2 my-4">

                        <router-link v-bind:to="product.get_absolute_url" class="btn btn-warning bold-btn">View details</router-link>

                    </div>
                </div>

            
            
            <!--             
            
            <h3 class="is-size-4">{{ product.name }}</h3>
            <p class="is-size-6 has-text-grey">₦{{ product.price }}</p>

            <router-link v-bind:to="product.get_absolute_url" class="button is-dark mt-4">View details</router-link>
             -->
        </div>
    </div>
</template>

<script>
export default {
    name: 'ProductBox',
    props: {
        product: Object
    }
}
</script>

<style scoped>
  .image {
    margin-top: -1.25rem;
    margin-left: -1.25rem;
    margin-right: -1.25rem;
  }

  img.card-img-top{
      border-radius: 15px;
  }
  .card-body {
      background: rgb(255, 255, 237);
  }
  .card{
      background: rgb(255, 255, 237);
      
  }
</style>