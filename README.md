# entregaEV3FF
# FragranceFantasy – Plataforma Móvil + Microservicios

## 1. Nombre del Proyecto
**FragranceFantasy**  
Aplicación móvil de e-commerce enfocada en perfumes, conectada a microservicios REST desarrollados en Spring Boot.

---

## 2. Integrantes
- **Franco Tamagnone**
- **Oriana Solorzano**

---

## 3. Funcionalidades Principales

### **App Móvil (Android – Kotlin + Jetpack Compose)**
- Registro de usuario vía API externa (microservicio de Autenticación).
- Login con obtención de token JWT.
- Visualización de catálogo de perfumes.
- Pantalla detallada del producto.
- Carrito de compras totalmente funcional.
- Realización de órdenes (checkout) consumiendo microservicios:
  - Microservicio de catálogo (precio real).
  - Microservicio de inventario (ajuste de stock).
  - Microservicio de órdenes (creación final).
- Pantalla de historial de pedidos (usuario autenticado).
- Conversión de precio usando API externa **Frankfurter** (cambio CLP → USD/EUR).

---

## 4. Endpoints Utilizados

### **Microservicio de Usuarios (Spring Boot – puerto 8084)**
- `POST /auth/register`
- `POST /auth/login`

### **Microservicio de Catálogo (Spring Boot – puerto 8083)**
- `GET /api/perfumes/{id}`  → obtener precio real del producto

### **Microservicio de Inventario (Spring Boot – puerto 8081)**
- `POST /api/inventario/ajustar-stock` → descontar stock / reponer al cancelar

### **Microservicio de Órdenes (Spring Boot – puerto 8080)**
- `POST /api/ordenes` → crear orden
- `GET /api/ordenes/{id}` → obtener detalle
- `GET /api/ordenes/usuario/{email}` → historial de órdenes
- `PUT /api/ordenes/{id}/completar`  
- `PUT /api/ordenes/{id}/cancelar`

### **API Externa – Frankfurter**
- `GET https://api.frankfurter.app/latest?amount={precio}&from=CLP&to=USD,EUR`

Usada para mostrar el valor del perfume en moneda extranjera.

---

## 5. Pasos para Ejecutar el Proyecto

### **A. Ejecutar Backend (microservicios)**

1. Clonar el repositorio de microservicios.
2. Asegurarse de tener **Java 17+** y **Maven** instalados.
3. Desde cada microservicio ejecutar:
   ```bash
   mvn spring-boot:run
4. Verificar con Swagger UI
  Usuarios	http://localhost:8084/swagger-ui.html
  Inventario	http://localhost:8081/swagger-ui.html
  Catálogo	http://localhost:8083/swagger-ui.html
  Órdenes	http://localhost:8080/swagger-ui.html
