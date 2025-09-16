<template>
  <div class="container-fluid mt-3" id="app">
    <div>
      <div class="form-group mb-4">
        <label for="nombreApellido">Nombre y/o apellido</label>
        <input
          type="text"
          id="nombreApellido"
          class="form-control"
          v-model="filtroNombreApellido"
          placeholder="Ingresar un nombre y/o apellido..."
        />
      </div>
      <div class="form-group">
        <label for="dni">DNI</label>
        <input
          type="number"
          id="dni"
          class="form-control"
          v-model="filtroDNI"
          placeholder="Ingresar un DNI.."
        />
      </div>
      <div v-if="mostrarAdvertencia" class="alert alert-warning">
        Debes ingresar al menos 3 caracteres en alguno de los filtros.
      </div>
    </div>
    <br />
    <div class="card-deck m-0">
      <div class="row">
        <div class="col" v-for="persona in personasFiltradas">
          <div class="card mb-3">
            <div class="card-body">
              <h5 class="card-title">{{ getNombreCompleto(persona) }}</h5>
              <p class="card-text">dni {{ persona.dni }}</p>
              <a href="#" class="card-link">{{ persona.correo }}</a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      filtroNombreApellido: "",
      filtroDNI: "",

      //Aquí, en este array es donde tienen que agregar su información
      personas: [
        {
          nombre: "Daniel",
          apellido: "Sanchez",
          correo: "danielsanchez68@hotmail.com",
          dni: "20442873",
        },
        {
          nombre: "Juan",
          apellido: "Perez",
          correo: "j@p.gmail.com",
          dni: "12345678",
        },
        {
          nombre: "Ana",
          apellido: "Suarez",
          correo: "a@s.gmail.com",
          dni: "87654321",
        },
        {
          nombre: "Tadeo",
          apellido: "Gavensky",
          correo: "tadeogavensky@gmail.com",
          dni: "43820991",
        },
      ],
    };
  },
  computed: {
    personasFiltradas() {
      return this.personas.filter((persona) => {
        const filtroActivoNombre = this.cumpleFiltroNombre;
        const filtroActivoDNI = this.cumpleFiltroDNI;

        const nombreCompleto =
          `${persona.nombre} ${persona.apellido}`.toLowerCase();

        const dni = persona.dni;

        const condicionNombre = filtroActivoNombre
          ? nombreCompleto.includes(this.filtroNombreApellido.toLowerCase())
          : true;

        const condicionDNI = filtroActivoDNI
          ? dni.includes(this.filtroDNI.toString())
          : true;

        return condicionNombre && condicionDNI;
      });
    },
    mostrarAdvertencia() {
      return !this.cumpleFiltroDNI && !this.cumpleFiltroNombre;
    },
    cumpleFiltroNombre() {
      return this.filtroNombreApellido.length >= 3;
    },
    cumpleFiltroDNI() {
      return this.filtroDNI.toString().length >= 3;
    },
  },
  methods: {
    getNombreCompleto(persona) {
      return `${persona.nombre} ${persona.apellido}`;
    },
  },
};
</script>

<style scoped></style>
