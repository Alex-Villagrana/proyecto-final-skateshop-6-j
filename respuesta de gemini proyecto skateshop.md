Este es un proyecto ambicioso que integra la arquitectura de agentes (SKILL.md) con un flujo de trabajo real en Flutter y Firebase. Para mantener la coherencia, configuraremos la estructura de la habilidad `.agents` orientada a la **Tienda de Skate**, asegurando que el entorno esté listo para un CRUD funcional.

---

## 1. Estructura de la Habilidad: `.agents/skate_shop`

Primero, definimos la estructura de carpetas que servirá como el "cerebro" de tu agente para este proyecto.

* **`.agents/skate_shop/SKILL.md`**: Define el comportamiento y reglas del agente.
* **`.agents/skate_shop/scripts/`**: Scripts de automatización (Bash/Python) para despliegue o limpieza.
* **`.agents/skate_shop/ejemplos/`**: Snippets de código de referencia.
* **`.agents/skate_shop/resources/`**: Activos, iconos de skates y configuración JSON.

---

## 2. Configuración del Entorno y Prerrequisitos

Antes de escribir código, debemos asegurar que las herramientas "hablen" entre sí.

### Verificación de Herramientas
Ejecuta esto en tu terminal de VS Code para confirmar que todo está en orden:

```bash
# Verificar Flutter
flutter --version

# Instalar Firebase CLI (si no lo tienes)
npm install -g firebase-tools

# Instalar FlutterFire CLI
dart pub global activate flutterfire_cli

# Login en Firebase
firebase login
```

> **Nota Crítica:** Una vez logueado, asegúrate de haber creado el proyecto en la [Consola de Firebase](https://console.firebase.google.com/) y activado **Firestore Database** en modo de prueba.

---

## 3. Creación del Proyecto y Conectividad

Configuraremos el proyecto base y lo vincularemos a Firebase automáticamente.

<Steps>
{/* Reason: El orden es crítico para evitar errores de vinculación entre el código de Flutter y los servicios de Firebase. */}
  <Step title="Crear el proyecto" subtitle="Carpeta principal">
    Ejecuta: `flutter create proyectoskateshop` y entra a la carpeta: `cd proyectoskateshop`.
  </Step>
  <Step title="Vincular con Firebase" subtitle="Configuración automática">
    Ejecuta: `flutterfire configure`. Selecciona tu proyecto creado en la consola y elige las plataformas (Android/iOS). Esto generará el archivo `firebase_options.dart`.
  </Step>
  <Step title="Instalar Dependencias" subtitle="Modificar pubspec.yaml">
    Añade estas líneas bajo `dependencies`:
    * `firebase_core: ^3.0.0`
    * `cloud_firestore: ^5.0.0`
  </Step>
</Steps>

---

## 4. Implementación del CRUD y UI (Dart)

Estructuraremos la carpeta `lib` para seguir una lógica limpia.

### Modelo de Datos: `lib/models/product_model.dart`
```dart
class Product {
  String id;
  String name;
  double price;
  String description;

  Product({required this.id, required this.name, required this.price, this.description = ""});

  Map<String, dynamic> toMap() => {
    "name": name,
    "price": price,
    "description": description,
  };

  factory Product.fromMap(String id, Map<String, dynamic> map) => Product(
    id: id,
    name: map['name'] ?? '',
    price: (map['price'] ?? 0).toDouble(),
    description: map['description'] ?? '',
  );
}
```

### Lógica de Firestore: `lib/services/firebase_service.dart`
```dart
import 'package:cloud_firestore/cloud_firestore.dart';
import '../models/product_model.dart';

class FirebaseService {
  final CollectionReference _db = FirebaseFirestore.instance.collection('productos');

  // CREATE
  Future<void> addProduct(Product product) => _db.add(product.toMap());

  // READ
  Stream<List<Product>> getProducts() {
    return _db.snapshots().map((snapshot) =>
        snapshot.docs.map((doc) => Product.fromMap(doc.id, doc.data() as Map<String, dynamic>)).toList());
  }

  // UPDATE
  Future<void> updateProduct(Product product) => _db.doc(product.id).update(product.toMap());

  // DELETE
  Future<void> deleteProduct(String id) => _db.doc(id).delete();
}
```

### Interfaz de Usuario: `lib/screens/home_screen.dart`
Crearemos una pantalla principal que muestre la lista y permita acciones CRUD.



```dart
// Resumen de la UI principal
// Se utiliza un StreamBuilder para escuchar cambios en tiempo real desde Firestore.
// Se implementa un FloatingActionButton para agregar nuevos Skates.
```

---

## 5. Archivo SKILL.md (El Agente Global)

Este archivo debe vivir en `.agents/skate_shop/SKILL.md` para que tu IDE (Antigravity/VS Code) entienda el contexto de la misión.

```markdown
# Skill: Skate Shop Automation Agent
**Contexto:** Desarrollo de App Flutter con Firebase Firestore.
**Objetivo:** Gestionar el CRUD de "proyectoskateshop".

## Reglas de Código
- Usar nombres descriptivos en Dart (CamelCase).
- Toda operación de datos debe pasar por `FirebaseService`.
- UI debe ser responsiva para móviles.

## Flujo de Trabajo
1. Verificar estado de Firebase login.
2. Ejecutar `flutter pub get` ante cambios en pubspec.
3. Generar vistas (Screens) antes de vincular lógica compleja.
```

---

<Elicitations message="El entorno está listo para empezar a programar. ¿Qué prefieres hacer a continuación?">
  <Elicitation label="Generar el código completo de la UI" query="Genera el código completo de home_screen.dart y product_form.dart para el CRUD de la tienda de skate con diseño moderno." />
  <Elicitation label="Configurar reglas de seguridad en Firestore" query="¿Cuáles son las reglas de seguridad recomendadas para la base de datos de Firestore en modo de desarrollo para esta app?" />
</Elicitations>
