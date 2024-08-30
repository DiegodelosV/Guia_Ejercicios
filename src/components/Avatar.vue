<template>
  <div>
    <div
      class="avatar"
      :style="{ 'background-image': 'url(' + foto + ')' }"
      @click="$emit('seleccionarAvatar')"
    ></div>
    <div>
      <button @click.prevent="$emit('eliminarFoto')">Eliminar</button>
    </div>
    <h1>{{ nombre }}</h1>
    <p>{{ email }}</p>
  </div>
</template>

<script>
export default {
  props: ["foto", "nombre", "email"],
};
</script>

<style scoped>
.avatar {
  width: 150px;
  height: 150px;
  background-size: cover;
  margin-top: 10px;
  margin-bottom: 10px;
  cursor: pointer; 
}
</style>
