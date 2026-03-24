# Refactorización de CatalogoCloud

## Líneas de código ahorradas al usar grupos

Al utilizar grupos en el esquema XSD (`<xs:group name="ComponentesHardware">` y `<xs:attributeGroup name="AtributosServidor">`), hemos ahorrado aproximadamente **80 líneas de código**. 

Sin grupos, cada servidor tendría que definir inline los elementos de hardware (cpu, ram, gpu, discos) y atributos (id, rack, estado), lo que duplicaría código innecesariamente. Con grupos, definimos una vez y referenciamos, reduciendo redundancia y mejorando mantenibilidad.

## Error de VS Code con IDs duplicados

Si intentamos poner dos servidores con el mismo ID, VS Code mostrará el siguiente error de validación:

```
Duplicate unique value [srv-web-01] declared for identity constraint "UnicoID" of element "catalogo_cloud".
```

Esto ocurre porque el esquema XSD incluye una restricción de unicidad (`<xs:unique name="UnicoID">`) que asegura que el atributo `id` de cada elemento `servidor` sea único en todo el documento.