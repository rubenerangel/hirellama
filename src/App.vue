<template>
  <div id="app">
    <div class="container">
      <!-- Image and text -->
      <nav class="navbar navbar-light bg-light">
        <a class="navbar-brand" href="#">
          <img src="https://www.hirellama.com/hubfs/raw_assets/public/Hire_Llama_August2020_v2/images/cropped-llama-09-1.png" width="250" height="50" class="d-inline-block align-top" alt="" loading="lazy">
          
        </a>
      </nav>

      <div class="row">
        <div class="col-8 mx-auto mt-2 p-3">
          <div class="card mx-auto" style="width: 18rem;">
            
            <div class="card-body">
              <h5 class="card-title">Enter the number</h5>
              <p class="card-text">After 2 seconds if the
                user hasn’t pressed any keys it should display on the page <span class="text-primary"> “Auto-saving”. </span>
              </p>
              <div class="input-group mb-3">
                <div class="input-group-prepend">
                  <span class="input-group-text" id="basic-addon1">Number</span>
                </div>
                <input 
                  @keypress="isNumber"
                  v-model="inputNumber"
                  ref="inputNumber"
                  type="text" 
                  class="form-control text-right" placeholder="0,00" aria-label="Username" aria-describedby="basic-addon1" autofocus>
              </div>
            </div>
          </div>
          <div class="col text-center text-primary h2">
            {{ textAutoSave }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import modalSave from "./components/modalSave.vue"
import $ from 'jquery'

export default {
  name: 'app',
  data () {
    return {
      lastKeyUpAt: new Date(),
      inputNumber: null,
      textAutoSave: ''
    }
  },
  methods: {
    isNumber($event) {
      this.textAutoSave = ''
      // Set key down time to the current time
      var keyDownAt = new Date();
      
      let keyCode = ($event.keyCode ? $event.keyCode : $event.which);
      if ((keyCode < 48 || keyCode > 57) && keyCode !== 46) { // 46 is dot
          $event.preventDefault();
      }else {
        setTimeout(() => {
          if (+keyDownAt > +this.lastKeyUpAt){
            this.inputNumber = null
            this.textAutoSave = 'Auto - Saving'
            this.$refs.inputNumber.focus()
          }
        }, 2000);
      }
    },
  }
}
</script>