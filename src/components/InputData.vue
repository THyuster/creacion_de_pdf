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
      function drawHeader(doc) {
        doc.addImage(imagenData, 'JPEG', 6, 6, 38, 20);
        doc.text('Direccion De Mantenimiento', 65, 13)
        doc.text('Actas De Mantenimiento Electrico', 61, 23)
        doc.text('NIT', 138, 10);
        doc.text('123456789-0', 132, 15);
        doc.text('Código de Factura', 128, 20); //el primer numero es para horiontal el segundo vertical
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
        doc.line(5, 28, doc.internal.pageSize.width - 5, 28); //linea de separacion
        doc.line(46, 17, doc.internal.pageSize.width - 5, 17); //linea de la mitad del recuadro
        doc.line(46, 5, 46, doc.internal.pageSize.height - 269); // linea de separacion cuadros con imagen
        doc.line(120, 5, 120, doc.internal.pageSize.height - 269); // linea de separacion parte media encabezado
        doc.line(120, 11, doc.internal.pageSize.width - 5, 11); //linea de la mitad para separacion de recuadros izquierdos
        doc.line(120, 23, doc.internal.pageSize.width - 5, 23); //linea de la mitad para separacion de recuadros izquierdos
        doc.line(160, 5, 160, doc.internal.pageSize.height - 269); // linea de separacion recuadros parte izquierda
      }

      // Función para dibujar la tabla
      function drawTable(doc, items, startY) {
        let margin = 10;
        let cellWidth = (doc.internal.pageSize.width - margin * 2) / 10;

        items.forEach((item, index) => {
          let currentY = startY + index * 10;

          doc.text(item.nombreEpp, margin, currentY);
          doc.text(item.parteCuerpoProteger, margin + cellWidth, currentY);
          doc.text(item.riesgoControlado, margin + cellWidth * 2, currentY);
          doc.text(item.cargoAsociado, margin + cellWidth * 3, currentY);
          doc.text(item.especificacionTecnica, margin + cellWidth * 4, currentY);
          doc.text(item.uso, margin + cellWidth * 5, currentY);
          doc.text(item.mantenimiento, margin + cellWidth * 6, currentY);
          doc.text(item.vidaUtil, margin + cellWidth * 7, currentY);
          doc.text(item.reposicion, margin + cellWidth * 8, currentY);
          doc.text(item.disposicionFinal, margin + cellWidth * 9, currentY);
        });

        for (let i = 0; i <= items.length + 1; i++) {
          doc.line(margin, startY + i * 10, margin + cellWidth * 10, startY + i * 10);
        }
        for (let i = 0; i <= 10; i++) {
          doc.line(margin + i * cellWidth, startY, margin + i * cellWidth, startY + (items.length + 1) * 10);
        }
      }

      // Función para generar páginas adicionales si la tabla excede el espacio de una página
      function generatePDFPages(doc, itemsPerPage, items) {
        let startY = 32;
        let margin = 10;

        let currentPageIndex = 0; // Índice de la página actual

        // Dibujar los bordes de la primera página fuera del bucle while
        drawBorders(doc);

        while (currentPageIndex * itemsPerPage < items.length) {
          if (currentPageIndex > 0) {
            // Si no es la primera página, agregamos una nueva página y dibujamos los bordes
            doc.addPage();
            startY = 15; // Restablecer el valor de startY para la nueva página
            drawBorders(doc); // Dibujar los bordes en la nueva página
          }

          let itemsOnPage = items.slice(currentPageIndex * itemsPerPage, (currentPageIndex + 1) * itemsPerPage);

          // Calcular la altura total que ocuparán las filas en la página
          let totalHeight = itemsOnPage.length * 10;

          // Verificar si el contenido supera el límite de altura de la página
          if (startY + totalHeight > 270) {
            // Si supera el límite, agregamos una nueva página
            doc.addPage();
            startY = 15; // Restablecer el valor de startY para la nueva página
            drawBorders(doc); // Dibujar los bordes en la nueva página
          }

          // Dibujar las filas en la página actual
          drawTable(doc, itemsOnPage, startY, margin);

          // Actualizar el valor de startY para la próxima iteración
          startY += totalHeight;

          // Incrementar el índice de la página actual
          currentPageIndex++;
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