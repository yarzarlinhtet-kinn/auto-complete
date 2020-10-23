<template>
  <div class="hello">
    <Autocomplete :suggestions="test" />
  </div>
</template>

<script>
import Autocomplete from './Autocomplete';
import zengin from 'zengin-code';
export default {
  name: 'HelloWorld',
  components: {
    Autocomplete,
  }, 
  data(){
    return {
      cities : [
            'Bangalore','Chennai','Cochin','Delhi','Kolkata','Mumbai', 'koko', 'kokoko'
        ],

      value: '',
      test: Object.values(zengin),
    }
  },
  props: {
    msg: String
  },
  mounted(){
    console.log(this.test);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
