<script>
  import { supabase } from "$lib/supabase.js";

  let email = "";
  let password = "";
  let username = "";
  let full_name = "";
  let last_name = "";
  let age = "";
  let city = "";
  let errorMessage = "";
  let message = "Bienvenido al registro para Conductores";
  $ : message

  async function signUpAndCreateProfile(
    email,
    password,
    username,
    full_name,
  ) {
    const { data, error } = await supabase.auth.signUp({ email, password });

    if (error) {
      console.error("Error signing up:", error);
      errorMessage = "Error signing up: " + error.message;
    } else if (data.user) {
      const { user } = data;
      const { error: profileError } = await supabase
        .from("driver_profile")
        .insert([
          { id: user.id, username, full_name, last_name, age, city },
        ]);

      if (profileError) {
        console.error("Error creating profile:", profileError);
        errorMessage = "Error creating profile: " + profileError.message;
      } else {
        message = "Conductor Creado";
        
      }
    }
  }

  async function register(event) {
    event.preventDefault();
    await signUpAndCreateProfile(email, password, username, full_name);
  }
</script>

<div
  class="alert alert-primary alert-dismissible fade show"
  role="alert"
>
  <button
    type="button"
    class="btn-close"
    data-bs-dismiss="alert"
    aria-label="Close"
  ></button>
  <strong>{message}</strong> 
</div>


<section>
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
        <div class="container d-flex justify-content-center">
          <form on:submit|preventDefault={register}>
            <div class="input-group mb-3">
              <input
                type="email"
                class="form-control"
                placeholder="Correo Electrónico"
                bind:value={email}
                aria-label="Correo Electrónico"
                aria-describedby="basic-addon2"
                required
              />
              <span class="input-group-text" id="basic-addon2"
                ><i class="fa-solid fa-envelope"></i></span
              >
            </div>

            <div class="input-group mb-3">
              <span class="input-group-text" id="basic-addon1"
                ><i class="fa-solid fa-lock"></i></span
              >
              <input
                type="password"
                class="form-control"
                placeholder="Contraseña"
                bind:value={password}
                aria-label="Contraseña"
                aria-describedby="basic-addon1"
                required
              />
            </div>

            <div class="input-group mb-3">
              <input
                type="text"
                class="form-control"
                placeholder="Username"
                bind:value={username}
                aria-label="Username"
                required
              />
            </div>

            <div class="input-group mb-3">
              <input
                type="text"
                class="form-control"
                placeholder="Nombres completos"
                bind:value={full_name}
                aria-label="Nombres completos"
                required
              />
            </div>

            <div class="input-group mb-3">
              <input
                type="text"
                class="form-control"
                placeholder="Apellidos Completos"
                bind:value={last_name}
                aria-label="Apellidos Completos"
                required
              />
            </div>

            <div class="input-group mb-3">
              <input
                type="text"
                class="form-control"
                placeholder="Edad"
                bind:value={age}
                aria-label="Edad"
                required
              />
            </div>

            <div class="input-group mb-3">
              <input
                type="text"
                class="form-control"
                placeholder="Ciudad de residencia"
                bind:value={city}
                aria-label="Ciudad de residencia"
                required
              />
            </div>

            <div class="d-flex justify-content-center">
              <button type="submit" class="btn btn-primary btn-lg"
                >Registrar</button
              >
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  @media (max-width: 992px) {
.h-custom {
height: 100%;
}
}
</style>
