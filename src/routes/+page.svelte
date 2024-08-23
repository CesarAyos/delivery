<script>
  import { supabase } from "$lib/supabase.js";
  import { goto } from "$app/navigation";
  import Footer from "../components/footer.svelte";

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
      goto("/users_profile");
    }
  }

  async function loginDriver(event) {
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

<div style="background:rgb(0,0,0,0.7);height: 100vh;">
  <div class="container p-5" >
    <div class="container mt-5 mb-5">
      <p class="text-center text-white" style="font-size: 50px;">
        VIAJA COMODO Y SEGURO
      </p>
      <p class="text-center text-white">Desde la comodidad de tu celular o ordenador</p>
    </div>

    <div class="container text-center pb-5">
      <div class="row row-cols-2 row-cols-lg-4 g-4 g-lg-3">
        <div class="col">
          <!-- Botón 1 -->
          <button
            type="button"
            class="btn btn-info text-white"
            data-bs-toggle="modal"
            data-bs-target="#modal1"
          >
            Iniciar sesion como usuario
          </button>

          <!-- Modal 1 -->
          <div
            class="modal fade"
            id="modal1"
            data-bs-backdrop="static"
            data-bs-keyboard="false"
            tabindex="-1"
            aria-labelledby="modal1Label"
            aria-hidden="true"
          >
            <div class="modal-dialog">
              <div class="modal-content">
                <div class="modal-header">
                  <h1 class="modal-title fs-5" id="modal1Label">
                    Iniciar sesion como usuario
                  </h1>
                  <button
                    type="button"
                    class="btn-close"
                    data-bs-dismiss="modal"
                    aria-label="Close"
                  ></button>
                </div>
                <div class="modal-body">
                  <section>
                    <div class="h-custom">
                      <div
                        class="row d-flex justify-content-center align-items-center h-100"
                      >
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
                              <label class="form-label" for="form3Example3"
                                >Correo Electrónico</label
                              >
                            </div>

                            <div data-mdb-input-init class="form-outline mb-3">
                              <input
                                type="password"
                                id="form3Example4"
                                class="form-control form-control-lg"
                                bind:value={password}
                                placeholder="Enter password"
                              />
                              <label class="form-label" for="form3Example4"
                                >Password</label
                              >
                            </div>

                            <div class="modal-footer">
                              <button
                                type="submit"
                                data-mdb-button-init
                                data-mdb-ripple-init
                                class="btn btn-primary btn-lg"
                                style="padding-left: 2.5rem; padding-right: 2.5rem;"
                                data-bs-dismiss="modal">Ingresar</button
                              >
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
                  </section>
                </div>
                <div class="modal-footer">
                  <button
                    type="button"
                    class="btn btn-secondary"
                    data-bs-dismiss="modal">Cerrar</button
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col">
          <!-- Botón 2 -->
          <button
            type="button"
            class="btn btn-info text-white"
            data-bs-toggle="modal"
            data-bs-target="#modal2"
          >
            iniciar sesion como conductor
          </button>

          <!-- Modal 2 -->
          <div
            class="modal fade"
            id="modal2"
            data-bs-backdrop="static"
            data-bs-keyboard="false"
            tabindex="-1"
            aria-labelledby="modal2Label"
            aria-hidden="true"
          >
            <div class="modal-dialog">
              <div class="modal-content">
                <div class="modal-header">
                  <h1 class="modal-title fs-5" id="modal2Label">
                    iniciar sesion como conductor
                  </h1>
                  <button
                    type="button"
                    class="btn-close"
                    data-bs-dismiss="modal"
                    aria-label="Close"
                  ></button>
                </div>
                <div class="modal-body">
                  <section>
                    <div class="h-custom">
                      <div
                        class="row d-flex justify-content-center align-items-center h-100"
                      >
                        <div class="col-md-9 col-lg-6 col-xl-5">
                          <!-- svelte-ignore a11y-img-redundant-alt -->
                          <img
                            src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-login-form/draw2.webp"
                            class="img-fluid"
                            alt="Sample image"
                          />
                        </div>
                        <div class="col-md-8 col-lg-6 col-xl-4 offset-xl-1">
                          <form on:submit|preventDefault={loginDriver}>
                            <div data-mdb-input-init class="form-outline mb-4">
                              <input
                                type="email"
                                id="form3Example3"
                                class="form-control form-control-lg"
                                placeholder="Enter a valid email address"
                                bind:value={email}
                              />
                              <label class="form-label" for="form3Example3"
                                >Correo Electrónico</label
                              >
                            </div>

                            <div data-mdb-input-init class="form-outline mb-3">
                              <input
                                type="password"
                                id="form3Example4"
                                class="form-control form-control-lg"
                                bind:value={password}
                                placeholder="Enter password"
                              />
                              <label class="form-label" for="form3Example4"
                                >Password</label
                              >
                            </div>
                            <div class="modal-footer">
                              <button
                                type="submit"
                                data-mdb-button-init
                                data-mdb-ripple-init
                                class="btn btn-primary btn-lg"
                                style="padding-left: 2.5rem; padding-right: 2.5rem;"
                                data-bs-dismiss="modal">Ingresar</button
                              >
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
                  </section>
                </div>
                <div class="modal-footer">
                  <button
                    type="button"
                    class="btn btn-secondary"
                    data-bs-dismiss="modal">Cerrar</button
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col">
          <!-- Botón 3 -->
          <button
            type="button"
            class="btn btn-info text-white"
            data-bs-toggle="modal"
            data-bs-target="#modal3"
          >
            Registrarse como usuario
          </button>

          <!-- Modal 3 -->
          <div
            class="modal fade"
            id="modal3"
            data-bs-backdrop="static"
            data-bs-keyboard="false"
            tabindex="-1"
            aria-labelledby="modal3Label"
            aria-hidden="true"
          >
            <div class="modal-dialog">
              <div class="modal-content">
                <div class="modal-header">
                  <h1 class="modal-title fs-5 text-dark" id="modal3Label">
                    Registro de usuario
                  </h1>
                  <button
                    type="button"
                    class="btn-close"
                    data-bs-dismiss="modal"
                    aria-label="Close"
                  ></button>
                </div>
                <div class="modal-body text-dark">
                  ¡Hola y bienvenidos a todos nuestros futuros clientes de
                  mototaxis! 🎉 Nos emociona que estés considerando unirte a
                  nuestra comunidad. Queremos asegurarnos de que tengas la mejor
                  experiencia posible, enfocándonos en la <strong
                    >seguridad</strong
                  >, la
                  <strong>Confianza</strong> y la <strong>comodidad</strong> de
                  nuestro servicio. Aquí van algunas recomendaciones para
                  comenzar: 1. <strong>Seguridad</strong>: Nuestros conductores
                  están capacitados y equipados con la indumentaria adecuada
                  para garantizar tu seguridad en cada viaje. Además, nuestras
                  motos son revisadas regularmente para asegurar su óptimo
                  funcionamiento. 2. <strong>Confianza</strong>: Puedes confiar
                  en nosotros para llegar a tu destino de manera rápida y
                  segura. Todos nuestros conductores están verificados y
                  comprometidos con ofrecer un servicio de calidad. 3.
                  <strong>comodidad</strong>: Disfruta de un viaje cómodo y sin
                  preocupaciones. Nos aseguramos de que cada trayecto sea lo más
                  agradable posible, adaptándonos a tus necesidades y
                  preferencias. Estamos aquí para ayudarte en todo lo que
                  necesites. ¡Gracias por confiar en nosotros y esperamos que
                  disfrutes de todos los beneficios de ser parte de nuestra
                  familia de mototaxis! 🌟 Si tienes alguna pregunta o necesitas
                  asistencia, no dudes en contactarnos. ¡Bienvenido y disfruta
                  de la experiencia! 🏍️💨
                </div>
                <div class="modal-footer">
                  <a href="user"
                    ><button
                      type="button"
                      class="btn btn-secondary"
                      data-bs-dismiss="modal">Registrarme</button
                    ></a
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="col">
          <!-- Botón 4 -->
          <button
            type="button"
            class="btn btn-info text-white"
            data-bs-toggle="modal"
            data-bs-target="#modal4"
          >
            Registrarse como conductor
          </button>

          <!-- Modal 4 -->
          <div
            class="modal fade"
            id="modal4"
            data-bs-backdrop="static"
            data-bs-keyboard="false"
            tabindex="-1"
            aria-labelledby="modal4Label"
            aria-hidden="true"
          >
            <div class="modal-dialog">
              <div class="modal-content">
                <div class="modal-header">
                  <h1 class="modal-title fs-5 text-dark" id="modal4Label">
                    Registrarme como conductor
                  </h1>
                  <button
                    type="button"
                    class="btn-close"
                    data-bs-dismiss="modal"
                    aria-label="Close"
                  ></button>
                </div>
                <div class="modal-body text-dark">
                  ¡Hola y bienvenidos a todos los futuros conductores de moto!
                  🚀 Nos alegra que estés interesado en unirte a nuestro equipo.
                  Antes de comenzar, queremos recordarte la importancia de la
                  <strong>Seguridad</strong> y la
                  <strong>indumentaria adecuada</strong>. Aquí hay algunos
                  puntos clave a tener en cuenta: 1. <strong>Casco</strong>:
                  Siempre usa un casco certificado para proteger tu cabeza. 2.
                  <strong>Ropa de protección</strong>: Lleva chaqueta, guantes,
                  pantalones y botas diseñados para la conducción en moto. 3.
                  <strong>Revisión del vehículo</strong>: Asegúrate de que tu
                  moto esté en perfectas condiciones antes de cada viaje. 4.
                  <strong>Respeto a las normas de tránsito</strong>: Sigue todas
                  las señales y reglas de tráfico para tu seguridad y la de los
                  demás. 5. <strong>Conducción defensiva</strong> : Mantente alerta
                  y anticipa las acciones de otros conductores. ¡Estamos emocionados
                  de tenerte con nosotros y esperamos que disfrutes de la experiencia
                  de conducir con seguridad y responsabilidad! 🏍️💨 Si tienes alguna
                  pregunta o necesitas más información, no dudes en contactarnos.
                  ¡Buena suerte y feliz conducción!
                </div>
                <div class="modal-footer">
                  <a href="driver">
                    <button
                      type="button"
                      class="btn btn-secondary"
                      data-bs-dismiss="modal">Registrarme</button
                    >
                  </a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
<Footer />


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
