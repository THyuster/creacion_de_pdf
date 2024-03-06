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
      <div>
        <label for="inspeccionEquipo">Inspección</label>
        <input type="text" id="inspeccionEquipo" name="inspeccionEquipo" v-model="inspeccionEquipo" placeholder="inspección">
      </div>
      <div>
        <label for="estadoEquipo">Estado</label>
        <select name="estadoEquipo" id="estadoEquipo" v-model="estadoEquipo">
          <option value="">Estado</option>
          <option value="Bueno">Bueno</option>
          <option value="Malo">Malo</option>
        </select>
      </div>
      <div>
        <label for="observacionesEquipo">Observaciones equipo</label>
        <input type="text" id="observacionesEquipo" name="observacionesEquipo" v-model="observacionesEquipo" placeholder="observaciones a Equipo">
      </div>
    </div>
  </div>
  <div class="contenedor_2">
      <div>
        <label for="UPM">UPM:  </label>
        <input v-model="UPM" id="UPM" name="UPM" placeholder=" UPM: " />
      </div>
    <div>
      <label for="marca">Marca: </label>
      <input v-model="marca" id="marca" name="marca" placeholder=" Marca:"/>
    </div>
    <div>
      <label for="activos_fijos">Activos Fijos:</label>
      <input v-model="activos_fijos" id="activos_fijos" name="activos_fijos" placeholder="Activos Fijos: " />
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
      <label for="fecha">Fecha</label>
      <input type="date" v-model="fecha" id="fecha" name="fecha" placeholder="Fecha " />
    </div>
    <div>
      <label for="hora">Hora: </label>
      <input type="time" id="hora" name="hora" v-model="hora" placeholder="Hora" />
    </div>
  </div>
  <div class="contenedor">
    <button @click="guardarItem">Guardar ítem</button>
    <button @click="generarPDF">Generar PDF</button>
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
        <tr v-for="(itemEq, index) in itemsEquipos" :key="index">
          <td>{{ itemEq.cambioEquipo }}</td>
          <td>{{ itemEq.realizadoEquipo }}</td>
          <td>{{ itemEq.cantidadEquipo }}</td>
          <td>{{ itemEq.referenciaEquipo }}</td>
        </tr>
      </tbody>
    </table>

    <table v-if="itemsInspeccionEquipos.length > 0">
      <thead>
        <tr>
          <th colspan="4">Inspección equipo</th>
        </tr>
        <tr>
          <th>Inspección</th>
          <th>Estado</th>
          <th>Observaciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(itemInspeccionEq, index) in itemsInspeccionEquipos" :key="index">
          <td>{{ itemInspeccionEq.inspeccionEquipo }}</td>
          <td>{{ itemInspeccionEq.estadoEquipo }}</td>
          <td>{{ itemInspeccionEq.observacionesEquipo }}</td>
        </tr>
      </tbody>
    </table>
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
      UPM: "1234567890",
      fecha: "04/03/2024",
      hora: "04:30 p.m.",
      marca: "Ferrari",
      activos_fijos: "No activo",
      cambioEquipo: 'bifo',
      realizadoEquipo: 'si',
      cantidadEquipo: '43634',
      referenciaEquipo: 'sdsg',
      inspeccionEquipo: 'rgw',
      estadoEquipo: 'Bueno',
      observacionesEquipo: 'ninguna',
      items: [],
      itemsEquipos: [],
      itemsInspeccionEquipos: [],
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
      if (this.cambioEquipo || this.realizadoEquipo || this.cantidadEquipo || this.referenciaEquipo) {
        this.itemsEquipos.push({
          cambioEquipo: this.cambioEquipo,
          realizadoEquipo: this.realizadoEquipo,
          cantidadEquipo: this.cantidadEquipo,
          referenciaEquipo: this.referenciaEquipo,
        });
      }
      if (this.inspeccionEquipo || this.estadoEquipo || this.observacionesEquipo) {
        this.itemsInspeccionEquipos.push({
          inspeccionEquipo: this.inspeccionEquipo,
          estadoEquipo: this.estadoEquipo,
          observacionesEquipo: this.observacionesEquipo,
        });
      }  
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
      this.cambioEquipo = "fg";
      this.realizadoEquipo = "si";
      this.cantidadEquipo = "43567";
      this.referenciaEquipo = "aifguk";
      this.inspeccionEquipo = "referencia";
      this.estadoEquipo = "bueno";
      this.observacionesEquipo = "aaaa";
    },
    async generarPDF() {
      const jsPDF = await import('jspdf');
      const doc = new jsPDF.default();

      doc.setDrawColor(0);
      doc.setLineWidth(0.2);
      doc.setFontSize(8);

      this.items.forEach(item => {
        if (item.hora && item.fecha && item.mantenimiento_realizado) {
          fechahoramatenimientoR(doc, item.hora, item.fecha, item.mantenimiento_realizado);
        }
      });

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
        doc.addImage(imagenData, 'PNG', 6, 6, 40, 20);
        doc.text('Direccion De Mantenimiento', 65, 13)
        doc.text('Actas De Mantenimiento Electrico', 61, 23)
        doc.text('NIT', 138, 9);
        doc.text('123456789-0', 132, 15);
        doc.text('Código de Factura', 130, 21);
        const codigoFactura = generarCodigoFactura(); // Generar código de factura
        doc.text(codigoFactura, 135, 27);// doc.setPage(1);
        const fechaActual = new Date().toLocaleDateString();
        doc.text('Fecha', 177, 21)
        doc.text(`${fechaActual}`, 175, 27);
        const totalPages = doc.internal.getNumberOfPages();
        doc.text('Página', 176, 9)
        for (let i = 1; i <= totalPages; i++) {
          doc.setPage(i);
          doc.text(`${i}`, doc.internal.pageSize.width - 30, 15);
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
      const fecha = this.fecha;
      const hora = this.hora;
      const marca = this.marca;
      fechahoramatenimientoR(doc, hora, fecha, mantenimiento_realizado, marca);

      function fechahoramatenimientoR (doc, hora, fecha, mantenimiento_realizado) {
        doc.text("Hora: ", 122, 46.5);
        doc.text(`${hora}`, 130, 46.5);
        doc.text("Fecha: ", 65, 46.5);
        doc.text(`${fecha}`, 75, 46.5);
        const tipoMantenimiento = mantenimiento_realizado ? (mantenimiento_realizado === 'Preventivo' ? 'Preventivo' : 'Correctivo') : ''; // Si no se ha seleccionado ninguno, dejar en blanco
        doc.text(`Mantenimiento Realizado: ${tipoMantenimiento}`, 8, 46.5);
      }
      const UPM = this.UPM;
      const activos_fijos = this.activos_fijos;

      drawEncabezado(doc, UPM, activos_fijos, marca);
      
      function drawEncabezado(doc, UPM, activos_fijos, marca) {
        doc.text("UPM:", 8, 33);
        doc.text(`${UPM}`, 16, 33);
        doc.text("Activo Fija:", 34, 33);
        doc.text(`${activos_fijos}`, 49, 33);
        doc.text("Marca:", 122, 33);
        doc.text(`${marca}`, 132, 33);
        doc.text("Serial: ", 8, 40);
        const codigoSerial = generarSerial();
        doc.text(codigoSerial, 180, 40);
        doc.line(5, 35, doc.internal.pageSize.width - 5, 35); //linea de separacion de upm hacia abajo
        doc.line(33, 28, 33, doc.internal.pageSize.height - 262); //linea vertical despues de upm
        doc.line(120, 28, 120, doc.internal.pageSize.height - 262); //linea vertical despues de upm
        doc.line(5, 42, doc.internal.pageSize.width - 5, 42); //linea de separacion de serial
        doc.line(5, 49, doc.internal.pageSize.width - 5, 49); // linea de sepracion de mantenimiento realizado
        doc.line(62, 49, 62, doc.internal.pageSize.height - 255); //linea vertical que separa mantenimiento realizado con la fecha
        doc.line(120, 49, 120, doc.internal.pageSize.height - 255); //linea vertical que separa fecha con horas        
      }
      // Dibujar el encabezado y los márgenes en la primera página
      drawBorders(doc);
      drawHeader(doc);

      // Calcular la posición de inicio de la segunda tabla
      const positionFirstTable = 49.5;
      const heightFirstTable = 2 + this.items.length * 6.8; // Asumiendo una altura de fila de 10

            // Llamada a la función drawFirstTable con this.items como argumento
      drawFirstTable(this.items);

      // Llamada a la función drawSecondTable con this.itemsEquipos como argumento
      drawSecondTable(this.itemsEquipos);

// Función para dibujar la primera tabla
function drawFirstTable(items) {
const pagePosition = doc.internal.getCurrentPageInfo().pageNumber;
    doc.autoTable({
        startY: positionFirstTable,
        head: [
            [{content: 'Caja de control', colSpan: 9, styles: {halign: 'center'}}],
            ['Nombre del EPP', 'Parte del Cuerpo a Proteger', 'Riesgo Controlado', 'Cargo Asociado', 'Especificación Técnica', 'Mantenimiento', 'Vida Útil', 'Reposición', 'Disposición Final']
        ],
        body: items.map(item => [
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
        theme: 'striped',
        margin: { top: 28.5, left: 5.5, right: 5.5 },
        styles: { fontSize: 8 },
        headerStyles: {
            textColor: '#000',
            fillColor: [200, 200, 200],
        },
        columnWidth: 'auto',
        didDrawPage: function () {
                const totalPages = doc.internal.getNumberOfPages();
                if (totalPages > pagePosition) {
                    drawHeader(doc);
                    drawBorders(doc);
                }
            }        
    });
}

// Función para dibujar la segunda tabla
function drawSecondTable(itemsEquipos) {
const pagePosition = doc.internal.getCurrentPageInfo().pageNumber;
    if (itemsEquipos.length > 0) {
        const positionSecondTableDynamic = positionFirstTable + heightFirstTable + 12;
        doc.autoTable({
            startY: positionSecondTableDynamic + 2.5,
            head: [
                [{content: 'Equipos', colSpan: 4, styles: {halign: 'center'}}],
                ['Cambio', 'Realizado', 'Cantidad', 'Referencia']
            ],
            body: itemsEquipos.map(itemEq => [
                itemEq.cambioEquipo,
                itemEq.realizadoEquipo,
                itemEq.cantidadEquipo,
                itemEq.referenciaEquipo,
            ]),
            theme: 'striped',
            margin: { top: 28.5, left: 5.5, right: 5.5 },
            styles: { fontSize: 8 },
            headerStyles: {
                textColor: '#000',
                fillColor: [200, 200, 200],
            },
            columnWidth: 'auto',
            didDrawPage: function () {
                const totalPages = doc.internal.getNumberOfPages();
                if (totalPages > pagePosition) {
                    drawHeader(doc);
                    drawBorders(doc);
                }
            } 
        });
    }
}

    // Guardar el documento
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
</style>
