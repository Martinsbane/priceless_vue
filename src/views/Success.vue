<template>
    <div class="page-success">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">Thank you</h1>

                <p>Your order will be processed within 48 hours</p>
                <hr>
                
                <router-link to="/"> 
                    <button class="button is-danger is-outlined"><strong>Back Home</strong></button>
                </router-link>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Success',
    mounted() {
        document.title = 'Success | Priceless'
    },
}
</script>