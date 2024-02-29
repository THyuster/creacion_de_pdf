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
import imagenData from '@/assets/LB-WORKS-NSX-NA113.jpg'
import 'jspdf-autotable';
export default {
  data() {
    return {
      nombreEpp: "",
      parteCuerpoProteger: "",
      riesgoControlado: "",
      cargoAsociado: "",
      especificacionTecnica: "",
      uso: "",
      mantenimiento: "",
      vidaUtil: "",
      reposicion: "",
      disposicionFinal: "",
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
      this.nombreEpp = "";
      this.parteCuerpoProteger = "";
      this.riesgoControlado = "";
      this.cargoAsociado = "";
      this.especificacionTecnica = "";
      this.uso = "";
      this.mantenimiento = "";
      this.vidaUtil = "";
      this.reposicion = "";
      this.disposicionFinal = "f";
    },
    async generarPDF() {
      
      const jsPDF = await import('jspdf')
      const pageSize = { width: 216, height: 279};
      const doc = new jsPDF.default();
      // const doc = new jsPDF({ format: [pageSize.width, pageSize.height] });

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

      let startY = 50;
      let remainingData = [
        ['Nombre del EPP', 'Parte del Cuerpo a Proteger', 'Riesgo Controlado', 'Cargo Asociado', 'Especificación Técnica', 'Uso', 'Mantenimiento', 'Vida Útil', 'Reposición', 'Disposición Final'],
        ...this.items.map(item => [
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
        ])
      ];

      while (remainingData.length > 0) {
        const availableSpace = pageSize.height - startY; 
        const maxRows = Math.floor(availableSpace / 20); 
        const rowsForPage = remainingData.slice(0, maxRows);

        doc.autoTable({
          startY: startY,
          head: [remainingData[0]],
          setFontSize: (8),
          body: rowsForPage,
          theme: 'grid'
        });

        remainingData = remainingData.slice(maxRows);

        if (remainingData.length > 0) {
          doc.addPage();
          startY = 10;
        }
      }

      // Función para generar páginas adicionales si la tabla excede el espacio de una página
      function generatePDFPages(doc, itemsPerPage, items) {
        if (items.length === 0) return;

        let startY = 48;
        let margin = 10;
        let currentPageIndex = 0;
        let isFirstPage = true;

        drawBorders(doc);

        while (currentPageIndex * itemsPerPage < items.length) {
          if (!isFirstPage) {
            doc.addPage();
            startY = 15;
            drawBorders(doc);
          }

          let itemsOnPage = items.slice(currentPageIndex * itemsPerPage, (currentPageIndex + 1) * itemsPerPage);

          let spaceLeft = doc.internal.pageSize.height - startY - margin;
          let totalHeight = itemsOnPage.length * 10;

          if (totalHeight > spaceLeft && !isFirstPage) {
            doc.addPage();
            startY = 15;
            drawBorders(doc);
          }

          startY += totalHeight;
          currentPageIndex++;
          isFirstPage = false;
        }
      }

      drawHeader(doc);
      drawBorders(doc);
      generatePDFPages(doc, this.itemsPerPage, this.items);

      doc.save("informacion.pdf");
    }
  }
};
</script>

<style>
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid black;
  padding: 8px;
}

th {
  background-color: #f2f2f2;
}
</style>