<script>
  import { goto } from "$app/navigation";
  import { supabase } from "$lib/supabase.js";
  import { onMount } from "svelte";

  let userProfile = null;
  let errorMessage = "";

  async function getUserSpace() {
    try {
      const { data: { session }, error } = await supabase.auth.getSession();

      if (error) {
        throw error;
      }

      if (session) {
        const userId = session.user.id;

        const { data: userProfileData, error: userProfileError } = await supabase
          .from("user_profiles")
          .select("*")
          .eq("id", userId)
          .maybeSingle();

        if (userProfileError) {
          throw userProfileError;
        } else if (userProfileData) {
          userProfile = userProfileData;
        } else {
          errorMessage = "No se encontró el perfil del usuario.";
          alert("No se encontro Usuario!")
          window.location.href = "/";
        }
      }
    } catch (error) {
      console.error("Error fetching session or user profile:", error);
      errorMessage = "Error fetching session or user profile: " + error.message;
    }
  }

  onMount(async () => {
    await getUserSpace();
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

  {#if userProfile}
    <div class="container d-flex justify-content-end">
      <button
        class="btn btn-outline-secondary"
        style="height: 35px;"
        type="button"
        data-bs-toggle="offcanvas"
        data-bs-target="#userProfileCanvas"
        aria-controls="userProfileCanvas"
      >
        Perfil de Usuario
      </button>
    </div>

    <div
      class="offcanvas offcanvas-start"
      data-bs-backdrop="static"
      tabindex="-1"
      id="userProfileCanvas"
      aria-labelledby="userProfileCanvasLabel"
    >
      <div class="offcanvas-header">
        <h5 class="offcanvas-title" id="userProfileCanvasLabel">
          Bienvenido: {userProfile.username}
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
          <p><strong>Nombre:</strong> {userProfile.full_name}</p>
          <p><strong>Apellidos:</strong> {userProfile.last_name}</p>
          <p><strong>Edad:</strong> {userProfile.age}</p>
          <p><strong>Residencia:</strong> {userProfile.city}</p>
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
