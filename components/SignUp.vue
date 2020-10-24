<template>
  <div class="tile is-child box">
    <div class="card">
      <header class="card-header">
        <p class="card-header-title is-centered has-background-info is-size-5">
          <strong class="has-text-white">Join the Party</strong>
        </p>
      </header>
      <div class="card-content is-info">
        <div class="content">
          <SignUpForm />
        </div>
        <footer class="card-footer">
          <p class="card-footer-item">
            <span>
              Share on
              <a
                target="_blank"
                href="https://twitter.com/intent/tweet?text=Check%20out%20Bounce%2C%20a%20website%20to%20help%20you%20find%20local%20basketball%20courts%21%20%23BounceMap"
                >Twitter</a
              >
            </span>
          </p>
          <p class="card-footer-item">
            <span>
              Share on
              <a
                target="_blank"
                href="https://www.facebook.com/sharer/sharer.php?u=https%3A%2F%2Fbouncemap.com%2F&amp;src=sdkpreparse"
                >Facebook</a
              >
            </span>
          </p>
        </footer>
      </div>
    </div>
  </div>
</template>


<script>
import SignUpForm from "../components/SignUpForm.vue";

export default {
  name: "Home",
  components: {
    SignUpForm,
  },
};
</script>


<style>
</style>
