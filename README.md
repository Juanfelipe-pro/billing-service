# 🧾 Servicio de Facturación y Control de Stock

> Proyecto backend en **Django + Django REST Framework**, diseñado con **principios SOLID**, arquitectura limpia y sistema de respuestas API unificado.

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python)
![Django](https://img.shields.io/badge/Django-5.x-green?logo=django)
![DRF](https://img.shields.io/badge/DRF-REST_Framework-red?logo=django)
![License](https://img.shields.io/badge/license-MIT-lightgrey)
![Status](https://img.shields.io/badge/status-en%20desarrollo-yellow)

---

## 🚀 Descripción

Aplicación REST que permite registrar **productos, proveedores, facturas y reportes de ventas**, implementando:

- 💡 **Principios SOLID**  
- ⚙️ **Transacciones atómicas** (`transaction.atomic`)
- 🔄 **Signals** para control automático de stock  
- 📊 **Reportes mensuales** con `annotate`, `F()`, y opción PDF  
- 🧱 **Arquitectura limpia**: `services`, `repositories`, `serializers`, `views`
- 📦 **Respuestas API unificadas** para integración con frontends o microservicios  

---

## 📂 Estructura del proyecto

```
billing/
├── models/
│   ├── product.py
│   ├── supplier.py
│   ├── invoice.py
│   ├── invoice_item.py
│
├── services/
│   ├── stock_service.py
│   ├── invoice_service.py
│   ├── report_service.py
│   └── pdf_service.py
│
├── repositories/
│   ├── product_repository.py
│   ├── invoice_repository.py
│
├── serializers/
│   ├── product_serializer.py
│   ├── invoice_serializer.py
│
├── views/
│   ├── product_view.py
│   ├── invoice_view.py
│   └── report_view.py
│
├── utils/
│   ├── api_response.py
│   └── exceptions.py
│
└── urls.py
```

---

## 🧠 Principios SOLID aplicados

| Principio | Implementación |
|------------|----------------|
| **S – Single Responsibility** | Cada clase/servicio tiene una única función |
| **O – Open/Closed** | Fácil de extender con nuevos reportes o servicios |
| **L – Liskov Substitution** | Servicios y repositorios intercambiables |
| **I – Interface Segregation** | Interfaces pequeñas y específicas |
| **D – Dependency Inversion** | Las vistas dependen de abstracciones, no del ORM |

---

## 📡 Endpoints principales

| Método | Ruta | Descripción |
|---------|------|-------------|
| `GET` | `/products/` | Listar productos |
| `POST` | `/products/` | Crear producto |
| `GET` | `/invoices/` | Listar facturas |
| `POST` | `/invoices/` | Crear factura con items |
| `GET` | `/reports/sales/?month=YYYY-MM` | Reporte mensual (JSON) |
| `GET` | `/reports/sales/pdf/?month=YYYY-MM` | Reporte mensual (PDF) |

---

## 📊 Ejemplo de respuesta estándar

### ✅ Éxito
```json
{
  "success": true,
  "data": {
    "id": 123,
    "name": "Producto creado correctamente"
  },
  "message": "Operación exitosa"
}
```

### ❌ Error
```json
{
  "success": false,
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Stock insuficiente",
    "details": ["El producto 'Monitor 27'' no tiene unidades disponibles"]
  }
}
```

---

## 🧾 Ejemplo de reporte `/reports/sales/?month=2025-10`

```json
{
  "success": true,
  "data": {
    "month": "2025-10",
    "total_sales": 15300000,
    "top_products": [
      {"product": "Monitor 27''", "qty": 45, "revenue": 6500000},
      {"product": "Mouse inalámbrico", "qty": 30, "revenue": 1500000}
    ]
  },
  "message": "Reporte generado exitosamente"
}
```

---

## ⚙️ Instalación local

```bash
git clone https://github.com/Juanfelipe-pro/billing-service.git
cd billing-service
python -m venv venv
source venv/bin/activate  # o venv\Scripts\activate en Windows
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

---

## 🧩 Stack Tecnológico

- **Python 3.12+**
- **Django 5.x**
- **Django REST Framework**
- **ReportLab / xhtml2pdf**
- **PostgreSQL o SQLite**
- **Docker Compose (opcional)**

---

## 🧪 Tests recomendados

- [ ] Creación de productos y facturas  
- [ ] Control de stock por `signal`  
- [ ] Rollback en fallas de transacción  
- [ ] Cálculo de totales con `F()` y `Sum()`  
- [ ] Reportes JSON y PDF correctos  

---

## 👨‍💻 Autor

**Juan Felipe Alvear**  
💼 Backend Developer — Python / Django / DRF / React  
🌍 Colombia 🇨🇴   
📎 [github.com/Juanfelipe-pro](https://github.com/Juanfelipe-pro)

---

## 📜 Licencia
MIT License — libre uso educativo y profesional.
