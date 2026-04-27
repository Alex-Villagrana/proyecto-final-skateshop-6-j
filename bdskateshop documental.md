```javascript
// Crear base de datos
use SkateShopDB
```

# 📌 Colecciones para un Skate Shop

## 1. Colección: productos

Guarda tablas, ropa, accesorios y tenis.

```javascript
db.createCollection("productos")
```

### Documento ejemplo:

```javascript
db.productos.insertOne({
    _id: ObjectId(),
    nombre: "Tabla Element 8.0",
    categoria: "Skateboard",
    marca: "Element",
    precio: 1299.99,
    stock: 15,
    talla: null,
    color: "Negro",
    material: "Maple Canadiense",
    fechaIngreso: new Date(),
    activo: true
})
```

### Atributos:

| Campo        | Tipo          |
| ------------ | ------------- |
| _id          | ObjectId      |
| nombre       | String        |
| categoria    | String        |
| marca        | String        |
| precio       | Decimal       |
| stock        | Int           |
| talla        | String / Null |
| color        | String        |
| material     | String        |
| fechaIngreso | Date          |
| activo       | Boolean       |

---

## 2. Colección: clientes

```javascript
db.createCollection("clientes")
```

### Documento ejemplo:

```javascript
db.clientes.insertOne({
    _id: ObjectId(),
    nombre: "Alejandro Torres",
    telefono: "6561234567",
    correo: "alex@email.com",
    direccion: {
        calle: "Av. Tecnológico",
        ciudad: "Juárez",
        estado: "Chihuahua"
    },
    fechaRegistro: new Date(),
    frecuente: true
})
```

### Atributos:

| Campo         | Tipo     |
| ------------- | -------- |
| _id           | ObjectId |
| nombre        | String   |
| telefono      | String   |
| correo        | String   |
| direccion     | Object   |
| fechaRegistro | Date     |
| frecuente     | Boolean  |

---

## 3. Colección: ventas

```javascript
db.createCollection("ventas")
```

### Documento ejemplo:

```javascript
db.ventas.insertOne({
    _id: ObjectId(),
    idCliente: ObjectId("ID_CLIENTE"),
    productos: [
        {
            idProducto: ObjectId("ID_PRODUCTO"),
            nombre: "Tabla Element 8.0",
            cantidad: 1,
            precioUnitario: 1299.99
        }
    ],
    total: 1299.99,
    metodoPago: "Tarjeta",
    fechaVenta: new Date()
})
```

### Atributos:

| Campo      | Tipo     |
| ---------- | -------- |
| _id        | ObjectId |
| idCliente  | ObjectId |
| productos  | Array    |
| total      | Decimal  |
| metodoPago | String   |
| fechaVenta | Date     |

---

## 4. Colección: empleados

```javascript
db.createCollection("empleados")
```

### Documento ejemplo:

```javascript
db.empleados.insertOne({
    _id: ObjectId(),
    nombre: "Carlos Ramírez",
    puesto: "Vendedor",
    sueldo: 8500,
    telefono: "6569876543",
    fechaIngreso: new Date(),
    activo: true
})
```

---

# 📌 Consultas básicas

## Ver productos

```javascript
db.productos.find()
```

## Buscar tablas disponibles

```javascript
db.productos.find({ categoria: "Skateboard", stock: { $gt: 0 } })
```

## Ventas mayores a $1000

```javascript
db.ventas.find({ total: { $gt: 1000 } })
```

---

# 📌 Recomendación profesional para Skate Shop

Colecciones ideales:

* productos
* clientes
* ventas
* empleados
* proveedores
* inventario
* marcas

---

# 📌 Si quieres, también puedo darte el **proyecto completo de Skate Shop en MongoDB con 50 registros reales para cada colección**, listo para entregar en la escuela.
