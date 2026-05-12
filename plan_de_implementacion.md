# 📱 Plan de Implementación: App "CompuCompra"
> **Stack:** Flutter + Dart | **Backend:** Firebase (Auth + Firestore) | **Estado:** Provider | **IDE:** VS Code  
> **Objetivo:** Aplicación multiplataforma de venta/compra de equipos de cómputo y accesorios con autenticación segura, gestión de catálogo, carrito de compras y sincronización en tiempo real.

---

## 🛠️ Herramientas Requeridas
| Categoría | Herramienta | Propósito |
|-----------|-------------|-----------|
| **Entorno** | Flutter SDK (última versión estable) | Framework base |
| | Dart SDK | Lenguaje de programación |
| | VS Code + Extensiones (Flutter, Dart, Firebase, Error Lens, Pubspec Assist) | Desarrollo y depuración |
| **Backend** | Firebase Console | Autenticación, Firestore, Analytics, Crashlytics |
| | Firebase CLI (`flutterfire`) | Configuración automática de credenciales |
| **Diseño** | Figma / Penpot | Wireframes, prototipos interactivos, design system |
| **Control de Versiones** | Git + GitHub/GitLab | Gestión de ramas, PRs, CI/CD |
| **Emuladores/Dispositivos** | Android Studio Emulator, iOS Simulator, Dispositivo físico | Pruebas multiplataforma |
| **Documentación** | Markdown, Notion/Obsidian | Seguimiento de tareas y decisiones técnicas |

> 📝 *Nota:* "Antigravity" no es un IDE reconocido para Flutter. Se recomienda **VS Code** como entorno principal por su ligereza y excelente integración con Dart/Flutter.

---

## 📦 Dependencias Planificadas (`pubspec.yaml`)
| Paquete | Versión Recomendada | Función |
|---------|---------------------|---------|
| `firebase_core` | ^2.x | Inicialización de Firebase |
| `firebase_auth` | ^4.x | Autenticación email/contraseña |
| `cloud_firestore` | ^4.x | Base de datos NoSQL en tiempo real |
| `provider` | ^6.x | Gestión de estado global |
| `go_router` | ^12.x | Enrutamiento declarativo y protegido |
| `flutter_form_builder` + `form_builder_validators` | ^9.x | Formularios con validación reutilizable |
| `cached_network_image` | ^3.x | Carga optimizada de imágenes de productos |
| `intl` | ^0.18.x | Formateo de moneda, fechas y localización |
| `shared_preferences` | ^2.x | Persistencia local ligera (carrito temporal, tema) |
| `flutter_launcher_icons` | ^0.13.x | Generación de íconos de app |
| `flutter_native_splash` | ^2.x | Pantalla de carga inicial |

> 🔒 Todas las versiones se mantendrán compatibles con la rama estable de Flutter. Se usarán restricciones `>=x.y.z <x.(y+1).0` para evitar rupturas.

---

## 🎨 UI/UX & Arquitectura
### 📐 Estructura de Carpetas (Conceptual)
```
lib/
├── core/          # Configuración, temas, constantes, utilidades
├── data/          # Repositorios, modelos, servicios Firebase
├── providers/     # ChangeNotifiers (Auth, Productos, Carrito, UI)
├── features/
│   ├── auth/      # Pantallas y lógica de login/registro
│   ├── home/      # Catálogo, búsqueda, filtros
│   ├── product/   # Detalle, reseñas, disponibilidad
│   ├── cart/      # Carrito, checkout simulado
│   └── profile/   # Historial, configuración, cerrar sesión
├── shared/        # Widgets reutilizables, componentes UI
└── main.dart      # Punto de entrada, inyección de Providers
```

### 🖌️ Principios UI/UX
- **Sistema de Diseño:** Material 3 con adaptaciones para iOS (cupertino donde aplique)
- **Paleta:** Tonos tecnológicos (azul eléctrico, gris carbón, blanco, acentos en verde éxito/rojo error)
- **Tipografía:** `Roboto` / `Inter` (jerarquía clara, tamaños responsivos)
- **Navegación:** BottomNavigationBar (móvil), NavigationRail (tablets/desktop)
- **Accesibilidad:** Contraste WCAG AA, soporte TalkBack/VoiceOver, tamaños de texto dinámicos
- **Feedback UX:** Indicadores de carga skeleton, toasts para acciones, estados vacíos ilustrados
- **Responsive:** Grids adaptativos (1-4 columnas según ancho), safe areas, keyboard handling

### 🧩 Arquitectura de Estado (Provider)
- `AuthProvider`: Expone `User?`, estado de sesión, métodos `login()`, `register()`, `logout()`, `resetPassword()`
- `ProductProvider`: Lista de productos, filtros, paginación, búsqueda, favoritos
- `CartProvider`: Items agregados, cantidades, cálculo de total, persistencia local/temporal
- `UIProvider`: Tema (claro/oscuro), estado de carga global, notificaciones internas
- **Separación clara:** Lógica de negocio en providers, UI pura en widgets, datos en repositorios

---

## 📋 Procedimiento Paso a Paso

### 🔹 Fase 1: Preparación del Entorno
1. Instalar Flutter SDK y verificar con `flutter doctor`
2. Configurar VS Code: instalar extensiones oficiales, activar formateo automático
3. Crear proyecto Flutter: `flutter create compucompra --org com.tuempresa`
4. Inicializar repositorio Git, crear ramas: `main`, `dev`, `feat/auth`, `feat/firestore`
5. Crear proyecto en Firebase Console, registrar apps Android, iOS y Web
6. Instalar Firebase CLI y ejecutar `flutterfire configure` para generar `firebase_options.dart`

✅ *Entregable:* Proyecto inicial funcional, Firebase vinculado, estructura Git lista

---

### 🔹 Fase 2: Configuración de Dependencias y Base
1. Agregar dependencias al `pubspec.yaml` (ver tabla anterior)
2. Ejecutar `flutter pub get` y verificar compatibilidad
3. Crear `core/` con: tema global, constantes de ruta, configuraciones de Firestore
4. Implementar pantalla de splash y navegación raíz con `go_router`
5. Configurar `flutter_native_splash` e ícono de app
6. Validar que la app compile en emulador Android e iOS

✅ *Entregable:* App base con navegación, tema, ícono y splash configurados

---

### 🔹 Fase 3: Diseño UI/UX y Prototipado
1. Disear wireframes en Figma para: Login, Registro, Home, Detalle Producto, Carrito, Perfil
2. Definir componentes reutilizables: `ProductCard`, `CustomButton`, `LoadingShimmer`, `EmptyState`
3. Establecer tokens de diseño: colores, espaciados, radios, sombras, elevaciones
4. Exportar assets optimizados (WebP, 1x/2x/3x)
5. Validar flujo de usuario con prototipo interactivo (click-through)

✅ *Entregable:* Design system documentado, prototipo validado, assets listos

---

### 🔹 Fase 4: Autenticación (Email/Password)
1. Habilitar Email/Password en Firebase Console → Authentication
2. Crear `AuthProvider` con `ChangeNotifier`
3. Implementar pantallas: `LoginScreen`, `RegisterScreen`, `ResetPasswordScreen`
4. Agregar validación de formularios, manejo de errores Firebase, estados de carga
5. Crear `AuthGuard` en rutas para proteger secciones privadas
6. Probar: registro, login, recuperación de contraseña, persistencia de sesión, cierre seguro

✅ *Entregable:* Flujo de autenticación completo, rutas protegidas, errores manejados

---

### 🔹 Fase 5: Integración con Firestore y State Management
1. Diseñar estructura de colecciones: `users`, `products`, `categories`, `orders`, `cart_items`
2. Configurar reglas de seguridad en Firestore (lectura/escritura por rol)
3. Crear repositorios: `ProductRepository`, `UserRepository`, `CartRepository`
4. Implementar `ProductProvider` y `CartProvider` con métodos CRUD básicos
5. Habilitar caché offline de Firestore y sincronización inteligente
6. Probar: inserción, lectura en tiempo real, filtrado básico, persistencia tras reinicio

✅ *Entregable:* Capa de datos funcional, proveedores operativos, seguridad configurada

---

### 🔹 Fase 6: Funcionalidades Core de "CompuCompra"
1. **Catálogo:** Grid responsivo, búsqueda por texto, filtros por categoría/precio
2. **Detalle:** Imágenes, especificaciones, disponibilidad, botón agregar al carrito
3. **Carrito:** Lista editable, cantidades, cálculo dinámico, botón checkout
4. **Perfil:** Datos de usuario, historial de compras, configuración de cuenta
5. **UX Refinamiento:** Skeleton loaders, pull-to-refresh, manejo de errores de red, animaciones suaves
6. **Pruebas de integración:** Flujo completo desde login hasta checkout simulado

✅ *Entregable:* App funcional con flujo de compra completo, optimizada y testeada

---

### 🔹 Fase 7: Testing, Optimización y Despliegue
1. Escribir pruebas unitarias para providers y repositorios
2. Pruebas de widgets para componentes críticos
3. Ejecutar en Firebase Test Lab (Android) y Simulator (iOS)
4. Optimizar rendimiento: lazy loading, `const` en widgets, reducción de rebuilds
5. Configurar Crashlytics y Analytics para monitoreo post-lanzamiento
6. Generar builds: `flutter build apk --release`, `flutter build ios --release`
7. Preparar metadatos para Play Store y App Store Connect
8. Implementar CI/CD básico (GitHub Actions o Codemagic)

✅ *Entregable:* App lista para distribución, monitoreada, con pipeline de releases

---

## ✅ Criterios de Aceptación Generales
- [ ] La app compila sin warnings críticos en al menos 2 plataformas
- [ ] Autenticación funciona con Firebase y maneja errores de red/credenciales
- [ ] Firestore sincroniza datos en <2s en condiciones normales de red
- [ ] Estado global no provoca rebuilds innecesarios (verificado con DevTools)
- [ ] Navegación respetada: rutas protegidas, historial controlado, deep linking listo
- [ ] UI accesible, responsiva y consistente con el design system
- [ ] Documentación interna actualizada (README, arquitectura, decisiones técnicas)

---

## 🔜 Siguientes Pasos
1. Revisar y aprobar este plan de implementación
2. Confirmar priorización de fases o ajustes de alcance
3. Solicitar el código por fase (ej: "Fase 4: Autenticación") y se entregará:
   - Estructura exacta de archivos
   - Implementación paso a paso con explicaciones
   - Snippets seguros y comentados
   - Pruebas y troubleshooting específicos

¿Deseas que procedamos con la **Fase 1 y 2 en código**, o prefieres ajustar algún alcance antes de comenzar la implementación técnica?
