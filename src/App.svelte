<script>
  import "bootstrap/dist/css/bootstrap.min.css";
  import "bootstrap-icons/font/bootstrap-icons.css";

  import { onMount } from "svelte";
  let personas = [];

  // Cargar los datos al montar el componente
  onMount(async () => {
    const response = await fetch("/data.json"); // Asumiendo que el archivo .json está en la raíz pública
    personas = await response.json();
  });

  function eliminarRegistro(idPersona) {
    console.log("Eliminar registro", idPersona);
    personas = personas.filter((persona) => persona.id !== idPersona);
  }
</script>

<div class="container">
  <div class="row">
    <div class="col">
      <h1 class="text-center fw-bold mb-5">
       Eliminar Registros Dinámicamente en una Tabla con Svelte <hr />
      </h1>

      <div class="table-responsive">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">#</th>
              <th scope="col">Nombre</th>
              <th scope="col">Teléfono</th>
              <th scope="col">Sexo</th>
              <th scope="col">Profesión</th>
              <th scope="col">Departamento</th>
              <th scope="col">Acción</th>
            </tr>
          </thead>
          <tbody>
            {#each personas as persona}
              <tr id={persona.id}>
                <th>{persona.id}</th>
                <td>{persona.nombre}</td>
                <td>{persona.telefono}</td>
                <td>{persona.Sexo}</td>
                <td>{persona.profesion}</td>
                <td>{persona.departamento}</td>
                <td>
                  <button
                    class="btn btn-warning"
                    type="button"
                    on:click={() => eliminarRegistro(persona.id)}
                    aria-label="Eliminar registro"
                  >
                    <i class="bi bi-trash"></i>
                  </button>
                </td>
              </tr>
            {/each}
          </tbody>
        </table>
      </div>
    </div>
  </div>
</div>
