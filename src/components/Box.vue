<script>
export default {

  name: "Box",

data() {
  return {

  };
},

props: {
    amount: Number,
    title: String,
},
methods: {

},
}

</script>

<template>
    <div class="col">
        <div class="card card-body">
            <h4> {{ title }}  </h4>
            <h5> $ {{ amount }} </h5>
        </div>
    </div>
</template>

<style scoped>

</style>
