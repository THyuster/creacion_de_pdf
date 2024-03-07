<template>
  <div class="contenedor">
    <div class="formularios_1">
      <label for="nombreEpp" id="nombre_epp">Nombre del EPP: </label>
      <input type="text" v-model="nombreEpp" placeholder="Nombre del EPP"/>
      <div>
        <label for="parteCuerpoProteger" id="parte_cuerpo_proteger">Parte del Cuerpo a Proteger</label>
        <input v-model="parteCuerpoProteger" placeholder="Parte del cuerpo a proteger" />
      </div>
      <div>
        <label for="riesgoControlado" id="riesgo_controlado">Riesgo Controlado</label>
        <input v-model="riesgoControlado" placeholder="Riesgo Controlado" />
      </div>
      <div>
        <label for="cargoAsociado" id="cargo_asociado">Cargo Asociado </label>
        <input v-model="cargoAsociado" placeholder="Cargo Asociado " />
      </div>
      <div>
        <label for="especificacion_Tecnica" id="especificacionTecnica">Especificación Técnica</label>
        <input v-model="especificacionTecnica" placeholder="Especificación Técnica"/>
      </div>
      <div>
        <label for="uso" id="uso">Uso </label>
        <input v-model="uso" placeholder="uso "/>
      </div>
      <div>
        <label for="mantenimiento" id="mantenimiento">Mantenimiento </label>
        <input v-model="mantenimiento" placeholder="Mantenimiento " />
      </div>
      <div>
        <label for="vida_Util" id="vidautil">Vida Útil </label>
        <input v-model="vidaUtil" placeholder="Vida Útil " />
      </div>
      <div>
        <label for="reposicion" id="reposicion"> Reposición </label>
        <input v-model="reposicion" placeholder=" Reposición " />
      </div>
      <div>
        <label for="disposicion_Final" id="disposicion_final"> Disposición Final </label>
        <input v-model="disposicionFinal" placeholder=" Disposición Final " />
      </div>
    </div>
    <div class="formularios_2">
      <div>
        <label for="cambioEquipo">Cambio</label>
        <input type="text" id="cambioEquipo" name="cambioEquipo" v-model="cambioEquipo" placeholder="Cambio">
      </div>
      <div>
        <label for="realizadoEquipo">Realizado</label>
        <select name="realizadoEquipo" id="realizadoEquipo" v-model="realizadoEquipo">
          <option value="">Realizado</option>
          <option value="Si" >Si</option>
          <option value="No">No</option>
        </select>
      </div>
      <div>
        <label for="cantidadEquipo">Cantidad</label>
        <input type="number" id="cantidadEquipo" name="cantidadEquipo" v-model="cantidadEquipo" placeholder="cambio">
      </div>
      <div>
        <label for="referenciaEquipo">Referencia</label>
        <input type="text" id="referenciaEquipo" name="referenciaEquipo" v-model="referenciaEquipo" placeholder="referencia">
      </div>
    </div>
    <div class="contenedor_2">
      <div>
        <label for="UPM" id="upm">UPM:  </label>
        <input v-model="UPM" placeholder=" UPM: " />
      </div>
    <div>
      <label for="Marca" id="upm">Marca: </label>
      <input v-model="marca" placeholder=" Marca:"/>
    </div>
    <div>
      <label for="activos_fijos" id="activos_fijos">Activos Fijos:</label>
      <input v-model="activos_fijos" placeholder="Activos Fijos: " />
    </div>
    <div>
        <label class="checkbox-label">Mantenimiento Realizado:</label>
        <label>
          <input type="radio" v-model="mantenimiento_realizado" value="Preventivo">
          Preventivo
        </label>
        <label>
          <input type="radio" v-model="mantenimiento_realizado" value="Correctivo">
          Correctivo
        </label>
      </div>
    <div>
      <label for="horometro" id="Horometro">Horometro </label>
      <input v-model="horometro" placeholder="Horometro " />
    </div>
    <div>
      <label for="fecha" id="fecha">Fecha</label>
      <input type="date" v-model="fecha" placeholder="Fecha " />
    </div>
  </div>
  <div class="contenedor">
    <button @click="guardarItem">Guardar ítem</button>
    <button @click="generarPDF">Generar PDF</button>
  </div>
</div>
  <div>
    <!-- Primera tabla -->
    <table>
      <thead>
        <tr>
          <th>Nombre del EPP</th>
          <th>Parte del Cuerpo a Proteger</th>
          <th>Riesgo Controlado</th>
          <th>Cargo Asociado</th>
          <th>Especificación Técnica</th>
          <th>Uso</th>
          <th>Mantenimiento</th>
          <th>Vida Útil</th>
          <th>Reposición</th>
          <th>Disposición Final</th>
          <th>UPM</th>
          <th>Activos Fijos</th>
          <th>Marca</th>
          <th>Mantenimiento Realizado</th>
          <th>Horometro</th>
          <th>Fecha</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in items" :key="index">
          <td>{{ item.nombreEpp }}</td>
          <td>{{ item.parteCuerpoProteger }}</td>
          <td>{{ item.riesgoControlado }}</td>
          <td>{{ item.cargoAsociado }}</td>
          <td>{{ item.especificacionTecnica }}</td>
          <td>{{ item.uso }}</td>
          <td>{{ item.mantenimiento }}</td>
          <td>{{ item.vidaUtil }}</td>
          <td>{{ item.reposicion }}</td>
          <td>{{ item.disposicionFinal }}</td>
          <td>{{ item.UPM }}</td>
          <td>{{ item.activos_fijos }}</td>
          <td>{{ item.marca }}</td>
          <td>{{ item.mantenimiento_realizado }}</td>
          <td>{{ item.horometro }}</td>
          <td>{{ item.fecha }}</td>
        </tr>
      </tbody>
    </table>

    <!-- Segunda tabla -->
    <table v-if="itemsEquipos.length > 0">
      <thead>
        <tr>
          <th colspan="4">Equipo</th>
        </tr>
        <tr>
          <th>Cambio</th>
          <th>Realizado</th>
          <th>Cantidad</th>
          <th>Referencia</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in itemsEquipos" :key="index">
          <td>{{ item.cambioEquipo }}</td>
          <td>{{ item.realizadoEquipo }}</td>
          <td>{{ item.cantidadEquipo }}</td>
          <td>{{ item.referenciaEquipo }}</td>
        </tr>
      </tbody>
    </table>
    <p v-else>No hay datos para mostrar en la segunda tabla.</p>
  </div>
</template><script>import { PDFDocument, rgb } from 'pdf-lib';
import { fetch } from 'cross-fetch';

export default {
  mounted() {
    this.generarPDF();
  },
  methods: {
    async generarPDF() {
      // Crear un nuevo documento PDF
      const pdfDoc = await PDFDocument.create();

      // Añadir una página al documento
      const page = pdfDoc.addPage();

      // Establecer el tamaño y la posición del texto en la página
      const x = 50;
      const y = page.getHeight() - 50;
      const fontSize = 12;

      // Escribir texto en la página
      page.drawText('Dirección De Mantenimiento', { x, y, size: fontSize, color: rgb(0, 0, 0) });
      page.drawText('Actas De Mantenimiento Electrico', { x, y: y - 15, size: fontSize, color: rgb(0, 0, 0) });

      // Obtener la imagen y añadirla al documento
      const imagenData = await fetch('ruta/de/tu/imagen.png').then(res => res.arrayBuffer());
      const imagen = await pdfDoc.embedPng(imagenData);
      page.drawImage(imagen, {
        x: 50,
        y: page.getHeight() - 80,
        width: 100,
        height: 50,
      });

      // Guardar el documento en un blob
      const pdfBytes = await pdfDoc.save();

      // Convertir los bytes del PDF a un blob
      const pdfBlob = new Blob([pdfBytes], { type: 'application/pdf' });

      // Descargar el blob como un archivo PDF
      const link = document.createElement('a');
      link.href = window.URL.createObjectURL(pdfBlob);
      link.download = 'informacion.pdf';
      link.click();
    }
  }
};
</script>
<style>
.contenedor {
  display: flex;
  justify-content: center;
}

.formularios_1, .formularios_2 {
  flex: 1;
  margin-right: 20px; 
}

/* Estilos para las tablas */
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 2%;
}

th, td {
  border: 1px solid black;
  padding: 8px;
}

th {
  background-color: #f2f2f2;
}
.contenedor_1{
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
  background-color: gray;
}
.contenedor_2 {
  position: relative;
  text-align: center;
  background-color: gray;
  width: 500px;
  margin-left: auto;
  margin-right: auto;
}
</style>