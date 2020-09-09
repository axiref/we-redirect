<template>
    <div class="v-redirect">
        <img class="timg tips-arrow" src="@/assets/tips-arrow.png">
        <div>
            请在浏览器打开
        </div>
    </div>
</template>

<script>
export default {

  name: 'Redirect',

  props: {
    browser: null,
  },

  data () {
    return {

    }
  }
}
</script>

<style lang="css" scoped>
@keyframes scale-a {
    0%{
        transform: scale(1);
    }
    25%{
        transform: scale(1.08);
    }
    50%{
        transform: scale(1);
    }
    75%{
        transform: scale(1.08);
    }
}
.timg
{
    width: 88%;
}
.tips-arrow
{
    -webkit-animation-name: scale-a;
    -webkit-animation-timing-function: ease-in-out;
    -webkit-animation-iteration-count: infinite;
    -webkit-animation-duration: 3s;
}
</style>