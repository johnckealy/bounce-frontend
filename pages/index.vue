<template>
  <div>
    <div>
      <br>
      <div class="tile is-ancestor">
        <div class="tile is-vertical is-parent content_box">
          <div class="tile">
            <div class="tile is-parent is-5 is-vertical">
              <div class="tile is-child box">
                <br>
                <p class="title">Bounce <i class="has-text-info is-size-4">Beta</i></p>
                <div class="content">
                  <p>
                    Let Bounce bring outdoor basketball courts to you!
                    Looking to find high quality outdoor basketball courts? Click <a href="/courts"><b>View Courts</b></a> to
                    view our map of over 45k searchable courts!
                  </p>
                  <br>
                  <p>Current and Future Features:</p>
                  <ul>
                      <li>Over 45k Courts</li>
                      <li>Multiple Map Themes</li>
                      <li>Rate and Comment on Basketball courts</li>
                      <li>Save your favorite courts</li>
                  </ul>
                </div>
              </div>
              <SignUp />
            </div>
            <Mapbox/>
          </div>
        </div>
      </div>
    </div>
    <br>
    <Footer />
  </div>
</template>




<script>

import Navbar from '../components/Navbar.vue'
import SignUp from '../components/SignUp.vue'
import Footer from '../components/Footer.vue'
import Mapbox from '../components/Mapbox.vue'

export default {

  name: 'Home', 
  components: {
    Navbar,
    SignUp,
    Footer,
    Mapbox
  }
}

</script>



<style>
</style>
