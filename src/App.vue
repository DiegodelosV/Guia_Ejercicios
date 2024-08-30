<script>
import Avatar from "./components/Avatar.vue";

export default {
  data() {
    return {
      avatares: [],
      nuevaFoto: "",
      nuevoNombre: "",
      nuevoEmail: "",
      avatarSeleccionado: null,
    };
  },
  components: {
    Avatar,
  },
  methods: {
    agregarAvatar() {
      const nuevoAvatar = {
        foto: this.nuevaFoto,
        nombre: this.nuevoNombre,
        email: this.nuevoEmail,
      };
      this.avatares.push(nuevoAvatar);
      this.nuevaFoto = "";
      this.nuevoNombre = "";
      this.nuevoEmail = "";
    },
    seleccionarAvatar(index) {
      this.avatarSeleccionado = this.avatares[index];
    },
  },
};
</script>

<template>
  <div class="contenedor">
    <form>
      <div><label for="nombre">Nombre</label></div>
      <input type="text" id="nombre" v-model="nuevoNombre" />
      <div><label for="foto">Foto</label> </div>
      <input type="text" id="foto" v-model="nuevaFoto" placeholder="URL" />
      <div><label for="email">Email</label></div>
      <input type="email" id="email" v-model="nuevoEmail" placeholder="ejemplo@email.com" />
      <div>
        <button @click.prevent="agregarAvatar">Agregar</button>
        <button @click.prevent="nuevaFoto = nuevoNombre = nuevoEmail = ''">
          Limpiar
        </button>
      </div>
      <div>
      <div v-for="(avatar, index) in avatares" :key="index">
        <Avatar
          :foto="avatar.foto"
          @eliminarFoto="avatares.splice(index, 1)"
          @seleccionarAvatar="seleccionarAvatar(index)"
        />
      </div>
    </div>
    </form>

    

    <section v-if="avatarSeleccionado">
      <div
        class="avatar-grande"
        :style="{ 'background-image': 'url(' + avatarSeleccionado.foto + ')' }"
      ></div>
      <h1>{{ avatarSeleccionado.nombre }}</h1>
      <p>{{ avatarSeleccionado.email }}</p>
    </section>
  </div>
</template>

<style scoped>
.contenedor {
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
}

form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin-top: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  color: white;
  background-color: #150c0c;
  width: 150px;
}

input {
  margin-bottom: 10px;
}

.avatar-grande {
  width: 300px;
  height: 300px;
  background-size: cover;
  background-position: center;
  margin-bottom: 10px;
  border-radius: 10px;
}

section {
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin-top: 10px;
  padding: 10px;
  border: 1px solid #150c0c;
  border-radius: 5px;
  background-color: white;
  margin-left: 20px;
}
</style>
