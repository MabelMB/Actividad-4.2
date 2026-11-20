<script setup lang="ts">
import { ref } from 'vue'

// Define datos
interface Item {
  id: number
  titulo: string
  valor: number
  detalles: { etiqueta: string; nota: number }[]
}

// Datos de prueba
const items = ref<Item[]>([
  {
    id: 1,
    titulo: 'Pensamiento Algorítmico',
    valor: 86,
    detalles: [
      { etiqueta: 'Parcial 1', nota: 100 },
      { etiqueta: 'Parcial 2', nota: 100 },
      { etiqueta: 'Parcial 3', nota: 100 },
      { etiqueta: 'Parcial 4', nota: 100 }
    ]
  },
  {
    id: 2,
    titulo: 'Diseño de Interfaces',
    valor: 100,
    detalles: [
      { etiqueta: 'Parcial 1', nota: 100 },
      { etiqueta: 'Parcial 2', nota: 100 },
      { etiqueta: 'Parcial 3', nota: 100 },
      { etiqueta: 'Parcial 4', nota: 100 }
    ]
  },
  {
    id: 3,
    titulo: 'Bases de datos',
    valor: 78,
    detalles: [
      { etiqueta: 'Parcial 1', nota: 100 },
      { etiqueta: 'Parcial 2', nota: 100 },
      { etiqueta: 'Parcial 3', nota: 100 },
      { etiqueta: 'Parcial 4', nota: 100 }
    ]
  },
  {
    id: 4,
    titulo: 'Robótica',
    valor: 78,
    detalles: [
      { etiqueta: 'Parcial 1', nota: 100 },
      { etiqueta: 'Parcial 2', nota: 100 },
      { etiqueta: 'Parcial 3', nota: 100 },
      { etiqueta: 'Parcial 4', nota: 100 }
    ]
  },
  {
    id: 5,
    titulo: 'Diseño web',
    valor: 78,
    detalles: [
      { etiqueta: 'Parcial 1', nota: 100 },
      { etiqueta: 'Parcial 2', nota: 100 },
      { etiqueta: 'Parcial 3', nota: 100 },
      { etiqueta: 'Parcial 4', nota: 100 }
    ]
  },
])

// Estado para saber cuál fila está abierta
const abiertoId = ref<number | null>(null)

function alternarFila(id: number) {
  abiertoId.value = abiertoId.value === id ? null : id
}
</script>

<template>

  <section class="card">
    <header class="card-header">
        <link rel="preconnect" href="https://googleapis.com">
        <link rel="preconnect" href="https://fonts.googleapis.com">
        <link href="https://googleapis.com/css2?family=Inter:wght@800&display=swap" rel="stylesheet">
      <h2>Calificaciones</h2>
    </header>

    <!-- Lista dinámica -->
    <div class="card-body">
      <div v-for="item in items" :key="item.id" class="fila-contenedor">
        <button class="fila-principal" :class="{ activa: abiertoId === item.id }" @click="alternarFila(item.id)">
          <span>
            <img src="../../assets/Chevron.png" class="chevron"/>
            {{ item.titulo }}</span>
          <span>{{ item.valor }}</span>
        </button>

        <!-- Sublista que aparece solo si esta fila está abierta -->
        <ul v-if="abiertoId === item.id" class="sublista">
          <li v-for="(det, index) in item.detalles" :key="index">
            <span>
              <img src="../../assets/circulo.png" class="circulo"/>
              {{ det.etiqueta }}</span>
            <span>{{ det.nota }}</span>
          </li>
        </ul>
      </div>
    </div>

    <footer class="card-footer">
      <button class="btn-accion">Regresar</button>
    </footer>
  </section>
</template>

<style scoped>
/* Estilos de la tarjeta */
.card-header{margin-bottom:10px; border-radius: 10px;}
.card { width: 100%; max-width: 800px; margin: 20px auto; overflow: hidden; }
.card-body { display: flex; flex-direction: column; gap: 8px; background-color: white; border-radius: 10px; overflow: hidden;}
.card-header { padding: 12px; text-align: center; background-color: #4EA8DE; color: black; font-family: 'Inter', sans-serif; font-weight: 800; font-style: normal; font-size: 13px; line-height: 24px; }
.fila-contenedor {width: 100%; background-color:pink}
.fila-principal {width:100%; padding: 15px;height: 34px;  display: flex; justify-content: space-between; background-color: #eff1ff; 
                border: none; padding: 10px; cursor: pointer; font-family: 'Inter', sans-serif; border: 3px solid transparent;}
                
.sublista {padding: 0; width:100%; margin: 0px; background-color:white; list-style: none;  font-family: 'Inter', sans-serif; display: flex; flex-direction: column; font-size:13px}
.sublista li { height: 20px; display: flex; justify-content: space-between; padding: 7px 10px; background-color:#DFF1FF}
.sublista li:nth-child(even) { background-color: white; }

.chevron { height: 87%; padding-right: 10px; padding-left: 5px; padding-right: 30px;}
.circulo { height: 25%; padding-right: 20px; padding-left: 7px; }

.fila-principal.activa {border-color: #165a8a;background-color: #ffffff;}
.card-footer { padding: 16px; display: flex; justify-content: center; }
.btn-accion{background-color: #1E6091; border-radius: 100px; color: white; box-shadow: 0 5px 20px -8px rgba(0, 0, 0, 0.50);
            padding: 10px 20px; border: none; cursor: pointer; font-family: 'Inter', sans-serif; font-weight: 500; font-style: normal; font-size: 14px;} 
</style>