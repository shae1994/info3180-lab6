<script>
import NewsList from '@/components/NewsList.vue'
export default {
    data() {
        return {
            message: "Hello World! Welcome to VueJS"
        };
    },
  components: { NewsList }
}
</script>

<template>
<div class="news container">
    <h2>News</h2>
    <br>
    <NewsList/>
    </div>
    
</template>



<style>
</style>