<script>
    import { supabase } from "$lib/supabase.js";
    import { goto } from "$app/navigation";
    let email = "";
    let password = "";
    let errorMessage = "";
  
    async function login(event) {
      event.preventDefault();
      const { data, error } = await supabase.auth.signInWithPassword({
        email,
        password,
      });
  
      if (error) {
        console.error("Error logging in:", error);
        errorMessage = "Error logging in: " + error.message;
      } else if (data.user) {
        console.log("User logged in:", data.user);
        goto("/drivers_profile");
      }
    }
  </script>
  
  <section class="vh-100">
    <div class="h-custom">
      <div class="row d-flex justify-content-center align-items-center h-100">
        <div class="col-md-9 col-lg-6 col-xl-5">
          <!-- svelte-ignore a11y-img-redundant-alt -->
          <img
            src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-login-form/draw2.webp"
            class="img-fluid"
            alt="Sample image"
          />
        </div>
        <div class="col-md-8 col-lg-6 col-xl-4 offset-xl-1">
          <form on:submit|preventDefault={login}>
            <div data-mdb-input-init class="form-outline mb-4">
              <input
                type="email"
                id="form3Example3"
                class="form-control form-control-lg"
                placeholder="Enter a valid email address"
                bind:value={email}
              />
              <label class="form-label" for="form3Example3">Correo Electrónico</label>
            </div>
  
            <div data-mdb-input-init class="form-outline mb-3">
              <input
                type="password"
                id="form3Example4"
                class="form-control form-control-lg"
                bind:value={password}
                placeholder="Enter password"
              />
              <label class="form-label" for="form3Example4">Password</label>
            </div>
  
            <div class="d-flex justify-content-between align-items-center">
              <!-- Checkbox -->
              <div class="form-check mb-0">
                <input
                  class="form-check-input me-2"
                  type="checkbox"
                  value=""
                  id="form2Example3"
                />
                <label class="form-check-label" for="form2Example3">
                  Recordar
                </label>
              </div>
              <a href="#!" class="text-body">Forgot password?</a>
            </div>
  
            <div class="text-center text-lg-start mt-4 pt-2">
              <button
                type="submit"
                data-mdb-button-init
                data-mdb-ripple-init
                class="btn btn-primary btn-lg"
                style="padding-left: 2.5rem; padding-right: 2.5rem;">Ingresar</button>
              <p class="small fw-bold mt-2 pt-1 mb-0">
                Aún no tienes una cuenta como conductor? <a href="driver" class="link-danger">Registrate</a>
              </p>
            </div>
          </form>
          {#if errorMessage}
            <div class="alert alert-danger mt-3" role="alert">
              {errorMessage}
            </div>
          {/if}
        </div>
      </div>
    </div>
    <div
      class="d-flex flex-column flex-md-row text-center text-md-start justify-content-between py-4 px-4 px-xl-5 bg-primary"
    >
      <!-- Copyright -->
      <div class="text-white">Copyright © 2020. All rights reserved.</div>
      <!-- Copyright -->
  
      <!-- Right -->
      <div>
        <a href="#!" class="text-white me-4">
          <i class="fab fa-facebook-f"></i>
        </a>
        <a href="#!" class="text-white me-4">
          <i class="fab fa-twitter"></i>
        </a>
        <a href="#!" class="text-white me-4">
          <i class="fab fa-google"></i>
        </a>
        <a href="#!" class="text-white">
          <i class="fab fa-linkedin-in"></i>
        </a>
      </div>
    </div>
  </section>
  
  
  {#if errorMessage}
    <p style="color: red;">{errorMessage}</p>
  {/if}
  
  <style>
    .h-custom {
      height: calc(100% - 73px);
    }
    @media (max-width: 992px) {
      .h-custom {
        height: 100%;
      }
    }
  </style>
  