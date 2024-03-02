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
</template>
<script>
import imagenData from '@/assets/logoMLA.png';
import 'jspdf-autotable';

export default {
  data() {
    return {
      nombreEpp: "elbo",
      parteCuerpoProteger: "fe",
      riesgoControlado: "feW",
      cargoAsociado: "EFW",
      especificacionTecnica: "gjg",
      uso: "ghd",
      mantenimiento: "fah",
      vidaUtil: "fhd",
      reposicion: "fdhd",
      disposicionFinal: "g",
      cambioEquipo: '',
      realizadoEquipo: '',
      cantidadEquipo: '',
      referenciaEquipo: '',
      itemsEquipos: [],
      itemsPerPage: 30,
      UPM: 'ss',
      activos_fijos: 'ss',
      marca: '',
      mantenimiento_realizado: '',
      horometro: 'ss',
      fecha: 'ss',
      items: [],
    };
  },
  methods: {
    guardarItem() {
      this.items.push({
        nombreEpp: this.nombreEpp,
        parteCuerpoProteger: this.parteCuerpoProteger,
        riesgoControlado: this.riesgoControlado,
        cargoAsociado: this.cargoAsociado,
        especificacionTecnica: this.especificacionTecnica,
        uso: this.uso,
        mantenimiento: this.mantenimiento,
        vidaUtil: this.vidaUtil,
        reposicion: this.reposicion,
        disposicionFinal: this.disposicionFinal,
        cambioEquipo: this.cambioEquipo,
        realizadoEquipo: this.realizadoEquipo,
        cantidadEquipo: this.cantidadEquipo,
        referenciaEquipo: this.referenciaEquipo,
        UPM: this.UPM,
        activos_fijos: this.activos_fijos,
        marca: this.marca,
        horometro: this.horometro,
        fecha: this.fecha,
      });      
      this.limpiarCampos();
    },
    limpiarCampos() {
      this.nombreEpp = "";
      this.parteCuerpoProteger = "";
      this.riesgoControlado = "";
      this.cargoAsociado = "";
      this.especificacionTecnica = "";
      this.uso = "";
      this.mantenimiento = "";
      this.vidaUtil = "";
      this.reposicion = "";
      this.disposicionFinal = "";
      this.UPM = 'ss';
      this.activos_fijos = 'ss';
      this.marca = "ss";
      this.mantenimiento_realizado = '';
      this.horometro = 'ss';
      this.fecha = 'ss';
      this.nombreEpp = "sdfh";
      this.parteCuerpoProteger = "sfhdd";
      this.riesgoControlado = "sdfh";
      this.cargoAsociado = "shdfd";
      this.especificacionTecnica = "sfhfd";
      this.uso = "hdsf";
      this.mantenimiento = "fdhsd";
      this.vidaUtil = "fhdf";
      this.reposicion = "gfh";
      this.disposicionFinal = "f";
      this.realizadoEquipo = "";
      this.UPM = 'ss';
      this.activos_fijos = 'ss';
      this.marca = "ss";
      this.mantenimiento_realizado = '';
      this.horometro = 'ss';
      this.fecha = 'ss';

    },
    async generarPDF() {
      const jsPDF = await import('jspdf');
      const doc = new jsPDF.default();

      doc.setDrawColor(0);
      doc.setLineWidth(0.2);
      doc.setFontSize(8);

      // Función para dibujar los márgenes de la página
      function drawBorders(doc) {
        doc.line(5, 5, doc.internal.pageSize.width - 5, 5);
        doc.line(5, 5, 5, doc.internal.pageSize.height - 5);
        doc.line(5, 292, doc.internal.pageSize.width - 5, 292);
        doc.line(205, 5, 205, doc.internal.pageSize.height - 5);
      }

      function generarCodigoFactura() {
        const caracteres = '1234567890';
        const longitud = 6;
        let codigo = '';
        for (let i = 0; i < longitud; i++) {
          const indice = Math.floor(Math.random() * caracteres.length);
          codigo += caracteres.charAt(indice);
        }
        return codigo;
      }

  // Dibujar el encabezado
  function drawHeader(doc) {
    doc.addImage(imagenData, 'JPEG', 6, 6, 38, 20);
    doc.text('Direccion De Mantenimiento', 65, 13)
    doc.text('Actas De Mantenimiento Electrico', 61, 23)
    doc.text('NIT', 138, 10);
    doc.text('123456789-0', 132, 15);
    doc.text("Codigo Factura", 130, 21);
    const codigoFactura = generarCodigoFactura(); // Generar código de factura
    doc.text(codigoFactura, 135, 27);// doc.setPage(1);
    const fechaActual = new Date().toLocaleDateString();
    doc.text('Fecha', 177, 21)
    doc.text(`${fechaActual}`, 175, 27);
    const totalPages = doc.internal.getNumberOfPages();
    doc.text('Paginas', 176, 9)
    for (let i = 1; i <= totalPages; i++) {
      doc.setPage(i);
      doc.text(`${i}`,  doc.internal.pageSize.width - 30, 15);
    }
    doc.line(5, 28, doc.internal.pageSize.width - 5, 28);
    doc.line(46, 17, doc.internal.pageSize.width - 5, 17);
    doc.line(46, 5, 46, doc.internal.pageSize.height - 269);
    doc.line(120, 5, 120, doc.internal.pageSize.height - 269);
    doc.line(120, 11, doc.internal.pageSize.width - 5, 11);
    doc.line(120, 23, doc.internal.pageSize.width - 5, 23);
    doc.line(160, 5, 160, doc.internal.pageSize.height - 269);
  }
  function generarSerial() {
        const caracteres = 'ABC1234567890';
        const longitud = 6;
        let serial = '';
        for (let i = 0; i < longitud; i++) {
          const indice = Math.floor(Math.random() * caracteres.length);
          serial += caracteres.charAt(indice);
        }
        return serial;
      }

      const mantenimiento_realizado = this.mantenimiento_realizado;

      drawEncabezado(doc, mantenimiento_realizado);
      
      function drawEncabezado(doc, mantenimiento_realizado){
        doc.text("UPM:", 8, 33);
        doc.text("Activo Fija:", 30, 33);
        doc.text("Marca:", 122, 33);
        doc.text("Serial: ", 8, 40);
        const codigoSerial = generarSerial();
        doc.text(codigoSerial, 180, 40);
        doc.text("Horometro", 120, 110);
        doc.text("Fecha", 120, 120);
        const tipoMantenimiento = mantenimiento_realizado ? (mantenimiento_realizado === 'Preventivo' ? 'Preventivo' :'Correctivo') : ''; // Si no se ha seleccionado ninguno, dejar en blanco
        doc.text(`Mantenimiento Realizado: ${tipoMantenimiento}`, 120, 100);
        doc.line(5, 35, doc.internal.pageSize.width - 5, 35); //linea de separacion de upm hacia abajo
        doc.line(26, 28, 26, doc.internal.pageSize.height - 262); //linea vertical despues de upm
        doc.line(120, 28, 120, doc.internal.pageSize.height - 262); //linea vertical despues de upm
        doc.line(5, 42, doc.internal.pageSize.width - 5, 42); //linea de separacion de serial
        doc.line(46, 70, doc.internal.pageSize.width - 5, 70); // linea de sepracion de mantenimiento realizado
        doc.line(46, 90, doc.internal.pageSize.width - 5, 90); // separacion de titulo 1
        doc.line(46, 110, doc.internal.pageSize.width - 5, 110); // separacion de titulo 2
      }
      // Dibujar el encabezado y los márgenes en la primera página
      drawBorders(doc);
      drawHeader(doc);

      // Guardar la posición y el número de página actual
      const firstPagePosition = doc.internal.getCurrentPageInfo().pageNumber;

      // Calcular la posición de inicio de la segunda tabla
      // const positionFirstTable = 28.5;
      const positionFirstTable = 80;
      const heightFirstTable = 2 + this.items.length * 6.8; // Asumiendo una altura de fila de 10

  doc.autoTable({
    startY: 80,
    head: [['Nombre del EPP', 'Parte del Cuerpo a Proteger', 'Riesgo Controlado', 'Cargo Asociado', 'Especificación Técnica', 'Uso', 'Mantenimiento', 'Vida Útil', 'Reposición', 'Disposición Final']], // Encabezado de la tabla
    body: this.items.map(item => [
      item.nombreEpp,
      item.parteCuerpoProteger,
      item.riesgoControlado,
      item.cargoAsociado,
      item.especificacionTecnica,
      item.uso,
      item.mantenimiento,
      item.vidaUtil,
      item.reposicion,
      item.disposicionFinal
    ]), // Datos de la tabla
    theme: 'grid', // Estilo de la tabla
    margin: { top: 28.5, left: 5.5, right: 5.5}, // Margen superior para evitar que se solape con el encabezado
    styles: { fontSize: 8 }, // Estilo de fuente para la tabla
    headerStyles: {
      textColor: '#000',
      fillColor: [200, 200, 200], // Color gris (F4F4F4)
    },
    columnWidth: 'auto', // Anchura automática para la primera columna
    didDrawPage: function () {
      // Verificar si hay más de una página adicional
      const totalPages = doc.internal.getNumberOfPages();
      if (totalPages > firstPagePosition) {
        // Iterar a través de las páginas adicionales y dibujar el encabezado y los márgenes
        for (let i = firstPagePosition + 1; i <= totalPages; i++) {
          doc.setPage(i);
          drawHeader(doc);
          drawBorders(doc);
        }
      }
    }
  });
      doc.autoTable({
        startY: positionFirstTable,
        head: [['Nombre del EPP', 'Parte del Cuerpo a Proteger', 'Riesgo Controlado', 'Cargo Asociado', 'Especificación Técnica', 'Mantenimiento', 'Vida Útil', 'Reposición', 'Disposición Final']], // Encabezado de la tabla
        body: this.items.map(item => [
          item.nombreEpp,
          item.parteCuerpoProteger,
          item.riesgoControlado,
          item.cargoAsociado,
          item.especificacionTecnica,
          item.mantenimiento,
          item.vidaUtil,
          item.reposicion,
          item.disposicionFinal,
        ]),
        theme: 'grid', // Estilo de la tabla
        margin: { top: 28.5, left: 5.5, right: 5.5 }, // Margen superior para evitar que se solape con el encabezado
        styles: { fontSize: 8 }, // Estilo de fuente para la tabla
        headerStyles: {
          textColor: '#000',
          fillColor: [200, 200, 200], // Color gris (F4F4F4)
        },
        columnWidth: 'auto', // Anchura automática para la primera columna
      });

      // Verificar si hay datos en la segunda tabla antes de agregarla al PDF
      let dataSecondTable = [];
    if (this.itemsEquipos.length > 0) {
      dataSecondTable = this.itemsEquipos.map(item => [
        item.cambioEquipo,
        item.realizadoEquipo,
        item.cantidadEquipo,
        item.referenciaEquipo,
      ]);
    }

  if (dataSecondTable.length > 0) {
    // Calcular la posición de inicio de la segunda tabla
    const positionSecondTableDynamic = positionFirstTable + heightFirstTable + 9; // Agregar un espacio entre tablas

    doc.autoTable({
      startY: positionSecondTableDynamic,
      head: [['Cambio', 'Realizado', 'Cantidad', 'Referencia']], // Encabezado de la segunda tabla
      body: dataSecondTable,
      theme: 'grid', // Estilo de la tabla
      margin: { top: 28.5, left: 5.5, right: 5.5 }, // Margen superior para evitar que se solape con el encabezado
      styles: { fontSize: 8 }, // Estilo de fuente para la tabla
      headerStyles: {
        textColor: '#000',
        fillColor: [200, 200, 200], // Color gris (F4F4F4)
      },
      columnWidth: 'auto',
      didDrawPage: function () {
        // Verificar si hay más de una página adicional
        const totalPages = doc.internal.getNumberOfPages();
        if (totalPages > firstPagePosition) {
          // Iterar a través de las páginas adicionales y dibujar el encabezado y los márgenes
          for (let i = firstPagePosition + 1; i <= totalPages; i++) {
            doc.setPage(i);
            drawHeader(doc);
            drawBorders(doc);
          }
        }
      }
    });
      }

      doc.save("informacion.pdf");
    }
  }
}
</script>

<style>
.contenedor {
  display: flex;
  justify-content: center;
}

.formularios_1, .formularios_2 {
  flex: 1;
  margin-right: 20px; /* Espacio entre los formularios */
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