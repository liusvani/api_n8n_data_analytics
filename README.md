# api_n8n_data_analytics

graph TD
    A[Trigger Manual] --> B[Get Ordenes (HTTP Request)]
    B --> C{Switch Node}
    C -->|Datos listos| D[Validación de datos (Code Node)]
    C -->|No existen órdenes| E[Notificar no existen datos (Gmail Node)]
    C -->|Error de conexión| F[Enviar reporte de error (Gmail Node)]
    D --> G[Transformar los datos (Code Node)]
    G --> H[Graficar datos (HTTP Request → QuickChart)]
    H --> I{If Node}
    I -->|Gráfico válido| J[Enviar reporte final (Gmail Node)]
    I -->|Falla gráfico| E
```
