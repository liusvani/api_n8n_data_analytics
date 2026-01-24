# API Data Analytics & Reporting Pipeline

Este workflow de **n8n** implementa un pipeline completo para la **validación, análisis y reporte de órdenes** provenientes de una API. Incluye validaciones de datos, generación de métricas, visualización gráfica y notificaciones automatizadas por correo electrónico.

---

## 🚀 Funcionalidades principales

- **Ingesta de datos**: Obtiene órdenes desde un endpoint configurable (`{{API_ENDPOINT_ORDERS}}`).
- **Validación robusta**: Verifica campos críticos (ID, nombre de cliente, teléfono, items de la orden).
- **Procesamiento de métricas**:
  - Órdenes pendientes, procesadas, completadas y canceladas.
  - Monto total de ventas (formateado en USD).
  - Producto más vendido.
- **Visualización automática**: Genera un gráfico tipo *doughnut* con [QuickChart](https://quickchart.io).
- **Notificaciones inteligentes**:
  - Reporte diario de ventas con métricas y gráfico.
  - Alertas de error de conexión con la API.
  - Aviso cuando la API responde sin datos.

---

## 🛠️ Requisitos previos

- Instancia de **n8n** (v1.121.3 o superior recomendado).
- Credenciales de Gmail configuradas en n8n:
  - Placeholder: `{{CREDENCIAL_GMAIL}}`
- Endpoint de API accesible:
  - Placeholder: `{{API_ENDPOINT_ORDERS}}`
- Dirección de correo destino:
  - Placeholder: `{{EMAIL_DESTINO}}`

---

## ⚙️ Configuración de placeholders

Antes de ejecutar el workflow, reemplaza los siguientes valores:

| Placeholder            | Descripción                                   | Ejemplo                          |
|------------------------|-----------------------------------------------|----------------------------------|
| `{{API_ENDPOINT_ORDERS}}` | URL de la API de órdenes                     | `http://mi-servidor:8484/orders` |
| `{{EMAIL_DESTINO}}`       | Correo electrónico para recibir reportes     | `equipo@empresa.com`             |
| `{{CREDENCIAL_GMAIL}}`    | Nombre de la credencial Gmail en n8n         | `Cuenta Gmail Corporativa`       |

---

## 📐 Flujo del pipeline

```mermaid
graph TD
    A[Schedule Trigger] --> B[Get Ordenes]
    B --> C[Switch]
    C --> D[Validación de datos]
    D --> E[Formatear para Gráfico]
    E --> F[Graficar datos]
    F --> G[If]
    G --> H[Envia reporte final]
    G --> I[Notificar no existen ordenes o fallo en API]
    C --> J[Enviar reporte de error]


