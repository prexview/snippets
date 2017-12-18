### Catálogos

#### Régimen fiscal

```html
{{_RegimenFiscal}}
```

```html
{{$mask _RegimenFiscal valueDelimiter="|" values="601|603|605|606|608|609|610|611|612|614|616|620|621|622|623|624|628|607|629|630|615" replaceWith="General de Ley Personas Morales|Personas Morales con Fines no Lucrativos|Sueldos y Salarios e Ingresos Asimilados a Salarios|Arrendamiento|Demás ingresos|Consolidación|Residentes en el Extranjero sin Establecimiento Permanente en México|Ingresos por Dividendos (socios y accionistas)|Personas Físicas con Actividades Empresariales y Profesionales|Ingresos por intereses|Sin obligaciones fiscales|Sociedades Cooperativas de Producción que optan por diferir sus ingresos|Incorporación Fiscal|Actividades Agrícolas, Ganaderas, Silvícolas y Pesqueras|Opcional para Grupos de Sociedades|Coordinados|Hidrocarburos|Régimen de Enajenación o Adquisición de Bienes|De los Regímenes Fiscales Preferentes y de las Empresas Multinacionales|Enajenación de acciones en bolsa de valores|Régimen de los ingresos por obtención de premios"}}
```

#### Tipo de comprobante

```html
{{_TipoDeComprobante}}
```

```html
{{$mask _TipoDeComprobante valueDelimiter="|" values="I|E|T|N|P" replaceWith="Ingreso|Egreso|Traslado|Nómina|Pago"}}
```

#### Uso del CFDI

```html
{{_UsoCFDI}}
```

```html
{{$mask _UsoCFDI valueDelimiter="|" values="G01|G02|G03|I01|I02|I03|I04|I05|I06|I07|I08|D01|D02|D03|D04|D05|D06|D07|D08|D09|D10|P01" replaceWith="Adquisición de mercancias|Devoluciones, descuentos o bonificaciones|Gastos en general|Construcciones|Mobilario y equipo de oficina por inversiones|Equipo de transporte|Equipo de computo y accesorios|Dados, troqueles, moldes, matrices y herramental|Comunicaciones telefónicas|Comunicaciones satelitales|Otra maquinaria y equipo|Honorarios médicos, dentales y gastos hospitalarios.|Gastos médicos por incapacidad o discapacidad|Gastos funerales.|Donativos.|Intereses reales efectivamente pagados por créditos hipotecarios (casa habitación).|Aportaciones voluntarias al SAR.|Primas por seguros de gastos médicos.|Gastos de transportación escolar obligatoria.|Depósitos en cuentas para el ahorro, primas que tengan como base planes de pensiones.|Pagos por servicios educativos (colegiaturas)|Por definir"}}
```


#### Impuesto

```html
{{_Impuesto}}
```

```html
{{$mask _Impuesto valueDelimiter="|" values="001|002|003" replaceWith="ISR|IVA|IEPS"}}
```


#### Método de pago

```html
{{_MetodoPago}}
```

```html
{{$mask _MetodoPago valueDelimiter="|" values="PUE|PPD" replaceWith="Pago en una sola exhibición|Pago en parcialidades o diferido"}}
```


#### Forma de pago

```html
{{_FormaPago}}
```

```html
{{$mask _FormaPago valueDelimiter="|" values="01|02|03|04|05|06|08|12|13|14|15|17|23|24|25|26|27|28|29|30|99" replaceWith="Efectivo|Cheque nominativo|Transferencia electrónica de fondos|Tarjeta de crédito|Monedero electrónico|Dinero electrónico|Vales de despensa|Dación en pago|Pago por subrogación|Pago por consignación|Condonación|Compensación|Novación|Confusión|Remisión de deuda|Prescripción o caducidad|A satisfacción del acreedor|Tarjeta de débito|Tarjeta de servicios|Aplicación de anticipos|Por definir"}}
```


#### Tipo de relación

```html
{{_TipoRelacion}}
```

```html
{{$mask _TipoRelacion valueDelimiter="|" values="01|02|03|04|05|06|07" replaceWith="Nota de crédito de los documentos relacionados|Nota de débito de los documentos relacionados|Devolución de mercancía sobre facturas o traslados previos|Sustitución de los CFDI previos|Traslados de mercancias facturados previamente|Factura generada por los traslados previos|CFDI por aplicación de anticipo"}}
```


#### QRCode

```html
{{#with Comprobante.Complemento.TimbreFiscalDigital}}
	{{$qrCode ($join "https://verificacfdi.facturaelectronica.sat.gob.mx/default.aspx?id=" _UUID "&re=" ../Comprobante.Emisor._Rfc "&rr=" ../Comprobante.Receptor._Rfc "&tt=" ../Comprobante._Total "&fe=" ($slice ../Comprobante._Sello -8)) fit=true}}
{{/with}}
```


#### Cadena original del timbre

```html
{{#with Comprobante.Complemento.TimbreFiscalDigital}}
	||{{_Version}}|{{_UUID}}|{{_FechaTimbrado}}|{{_RfcProvCertif}}|{{_SelloCFD}}|{{_NoCertificadoSAT}}||
{{/with}}
```

### Formatos

#### Fecha y hora en español

```html
{{$capitalize ($date _Fecha format="DD MMM YYYY [-] H:mm:ss" locale="es")}}
```

### Catálogos - Complemento - Servicios parciales de construcción

#### Estado

```html
{{Estado}}
```

```html
{{$mask Estado valueDelimiter="|" values="01|02|03|04|05|06|07|08|09|10|11|12|13|14|15|16|17|18|19|20|21|22|23|24|25|26|27|28|29|30|31|32" replaceWith="Aguascalientes|Baja California|Baja California Sur|Campeche|Coahuila de Zaragoza|Colima|Chiapas|Chihuahua|Distrito Federal|Durango|Guanajuato|Guerrero|Hidalgo|Jalisco|México|Michoacán de Ocampo|Morelos|Nayarit|Nuevo León|Oaxaca|Puebla|Querétaro|Querétaro Roo|San Luis Potosí|Sinaloa|Sonora|Tabasco|Tamaulipas|Tlaxcala|Veracruz de Ignacio de la Llave|Yucatán|Zacatecas"}}
```

### Información más compleja

#### Extra valor

Imprimir un extra valor cuando el atributo sea igual a un valor especifico ejemplo, imprimir el valor del nodo cuando el atributo sea "sucursal"

```html
{{#each Addenda.AddendaBuzonFiscal.Extra}}
	{{#switch _atributo}}
		{{#case "sucursal"}}
			<div>{{_valor}}</div>
		{{/case}}
	{{/switch}}
{{/each}}
```
