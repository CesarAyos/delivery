<script>
  import { supabase } from "$lib/supabase.js";
  import { onMount } from "svelte";

  let driverProfile = null;
  let errorMessage = "";

  async function getUserSpace() {
    try {
      const { data: { session }, error } = await supabase.auth.getSession();

      if (error) {
        console.error("Error fetching session:", error);
        errorMessage = "Error fetching session: " + error.message;
        return;
      }

      if (session) {
        const userId = session.user.id;

        const { data: driverProfileData, error: driverProfileError } = await supabase
          .from("driver_profile")
          .select("*")
          .eq("id", userId)
          .maybeSingle();

        if (driverProfileError) {
          throw driverProfileError;
        } else if (driverProfileData) {
          driverProfile = driverProfileData;
        } else {
          errorMessage = "No se encontró el perfil del usuario.";
          alert("No se encontró Usuario!");
          window.location.href = "/";
        }
      }
    } catch (error) {
      console.error("Error fetching session or user profile:", error);
      errorMessage = "Error fetching session or user profile: " + error.message;
    }
  }

  onMount(() => {
    getUserSpace();
  });

  const handleLogout = async () => {
    await supabase.auth.signOut();
    window.location.href = "/";
  };
</script>

<div>
  {#if errorMessage}
    <div class="alert alert-danger" role="alert">
      {errorMessage}
    </div>
  {/if}

  {#if driverProfile}
    <div class="container d-flex justify-content-end">
      <button
        class="btn btn-outline-secondary"
        style="height: 35px;"
        type="button"
        data-bs-toggle="offcanvas"
        data-bs-target="#driverProfileCanvas"
        aria-controls="driverProfileCanvas"
      >
        Perfil de Usuario
      </button>
    </div>

    <div
      class="offcanvas offcanvas-start"
      data-bs-backdrop="static"
      tabindex="-1"
      id="driverProfileCanvas"
      aria-labelledby="driverProfileCanvasLabel"
    >
      <div class="offcanvas-header">
        <h5 class="offcanvas-title" id="driverProfileCanvasLabel">
          Bienvenido: {driverProfile.username}
        </h5>
        <button
          type="button"
          class="btn-close"
          data-bs-dismiss="offcanvas"
          aria-label="Close"
        ></button>
      </div>
      <div class="offcanvas-body">
        <div>
          <p><strong>Nombre:</strong> {driverProfile.full_name}</p>
          <div><strong>Apellidos:</strong> {driverProfile.last_name}</div>
          <p><strong>Edad:</strong> {driverProfile.age}</p>
          <p><strong>Residencia:</strong> {driverProfile.city}</p>
        </div>
        <button
          type="button"
          class="btn btn-danger"
          style="border-radius:20px;"
          on:click={handleLogout}
        >
          Cerrar sesión
        </button>
      </div>
    </div>
  {/if}
</div>
