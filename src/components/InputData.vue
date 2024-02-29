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
  </div>
</template>

<script>
import imagenData from '@/assets/LB-WORKS-NSX-NA113.jpg'; 
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
      this.disposicionFinal = "";
    },
    async generarPDF() {
      const jsPDF = await import('jspdf');
      const doc = new jsPDF.default();

      doc.setFontSize(8);
      doc.setDrawColor(0); 
      doc.setLineWidth(0.2); 

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
      

      drawBorders(doc);
      drawHeader(doc);

      this.items.forEach((item, index) => {
        doc.text(`Nombre del EPP: ${item.nombreEpp}`, 10, 60 + (index * 100));
        doc.text(`Parte del Cuerpo a Proteger: ${item.parteCuerpoProteger}`, 10, 70 + (index * 100));
        doc.text(`Riesgo Controlado: ${item.riesgoControlado}`, 10, 80 + (index * 100));
        doc.text(`Cargo Asociado: ${item.cargoAsociado}`, 10, 90 + (index * 100));
        doc.text(`Especificacion Tecnica: ${item.especificacionTecnica}`, 10, 100 + (index * 100));
        doc.text(`Uso: ${item.uso}`, 10, 110 + (index * 100));
        doc.text(`Mantenimiento: ${item.mantenimiento}`, 10, 120 + (index * 100));
        doc.text(`Vida Util: ${item.vidaUtil}`, 10, 130 + (index * 100));
        doc.text(`Reposicion: ${item.reposicion}`, 10, 140 + (index * 100));
        doc.text(`Disposicion Final: ${item.disposicionFinal}`, 10, 150 + (index * 100));
      });

      doc.save("informacion.pdf");
    }
  }
};
</script>

<style>
</style>
