<template>
    <footer class="footer py-3 bg-light">
        <div class="container">
            <p class="text-muted">Copyright &copy; {{year}} Mendy Katz All Rights Reserved</p>
        </div>
    </footer>
</template>

<script>
export default {
    name: 'Footer',
    data(){
        return{
            year: Number
        }
    },
    created() {
     this.year = new Date().getFullYear()
  }
    
}
</script>

<style scoped>
    .footer{
        position: fixed;
        left: 0;
        bottom: 0;
        width: 100%;
        text-align: center;
    }
</style>