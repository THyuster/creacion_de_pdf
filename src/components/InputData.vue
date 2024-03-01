<template>
  <div>
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
      <input v-model="especificacionTecnica" placeholder="Especificación Técnica " />
    </div>
    <div>
      <label for="uso" id="uso">Uso </label>
      <input v-model="uso" placeholder="uso " />
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
    <button @click="guardarItem">Guardar ítem</button>
    <button @click="generarPDF">Generar PDF</button>
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
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
import imagenData from '@/assets/LB-WORKS-NSX-NA113.jpg';
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
      items: [],
      itemsPerPage: 30,
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
      });
      this.limpiarCampos();
    },
    limpiarCampos() {
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

  // Dibujar el encabezado
  function drawHeader(doc) {
    doc.addImage(imagenData, 'JPEG', 6, 6, 38, 20);
    doc.text('Direccion De Mantenimiento', 65, 13)
    doc.text('Actas De Mantenimiento Electrico', 61, 23)
    doc.text('NIT', 138, 10);
    doc.text('123456789-0', 132, 15);
    doc.text('Código de Factura', 128, 20);
    doc.text('ABC123', 135, 27)
    const fechaActual = new Date().toLocaleDateString();
    doc.text('Fecha', 177, 21)
    doc.text(`${fechaActual}`, 175, 27);
    const totalPages = doc.internal.getNumberOfPages();
    doc.text('Paginas', 176, 9)
    for (let i = 1; i <= totalPages; i++) {
      doc.setPage(i);
      doc.text(`${i} de ${totalPages}`, doc.internal.pageSize.width - 33, 15);
    }
    doc.line(5, 28, doc.internal.pageSize.width - 5, 28);
    doc.line(46, 17, doc.internal.pageSize.width - 5, 17);
    doc.line(46, 5, 46, doc.internal.pageSize.height - 269);
    doc.line(120, 5, 120, doc.internal.pageSize.height - 269);
    doc.line(120, 11, doc.internal.pageSize.width - 5, 11);
    doc.line(120, 23, doc.internal.pageSize.width - 5, 23);
    doc.line(160, 5, 160, doc.internal.pageSize.height - 269);
  }

  // Dibujar el encabezado y los márgenes en la primera página
  drawBorders(doc);
  drawHeader(doc);

  // Guardar la posición y el número de página actual
  const firstPagePosition = doc.internal.getCurrentPageInfo().pageNumber;

  doc.autoTable({
    startY: 28.5,
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

  doc.save("informacion.pdf");
}
  }
}
</script>

<style>
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
</style>