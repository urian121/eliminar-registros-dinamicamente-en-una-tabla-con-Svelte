<script>
  import "bootstrap/dist/css/bootstrap.min.css";
  import "bootstrap-icons/font/bootstrap-icons.css";

  import { onMount } from "svelte";
  let personas = [];

  onMount(async () => {
    // Realiza una solicitud para obtener los datos del archivo JSON ubicado en la raíz pública
    const response = await fetch("/data.json");

    // Convierte la respuesta en formato JSON y asigna los datos al arreglo 'personas'
    personas = await response.json();
  });

  function eliminarRegistro(idPersona) {
    // Imprime el ID de la persona que se va a eliminar (para fines de depuración)
    console.log("Eliminar registro con ID:", idPersona);

    // Filtra el arreglo 'personas' para eliminar el registro con el ID correspondiente
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
