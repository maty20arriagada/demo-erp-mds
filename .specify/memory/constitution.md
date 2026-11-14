<!--
Sync Impact Report
- Version change: 1.0.0 (genérica) → 1.0.0 (proyecto ERP Inventario)
- Modified principles: Reemplazadas las 4 principles genéricas por 6 principles propias del proyecto (Español, localStorage, Vitest-first, Accesibilidad, Datos sensibles y sesgos, Trazabilidad en GitHub Issues).
- Added sections: Restricciones de proyecto, Flujo de trabajo por historias
- Removed sections: Ninguna (las principles genéricas quedan absorbidas por las nuevas)
- Templates requiring updates: ✅ .specify/templates/plan-template.md, ✅ .specify/templates/spec-template.md, ✅ .specify/templates/tasks-template.md (sin cambios estructurales: los principios existentes de cobertura y verificación se mantienen y ahora apuntan a Vitest y a Issues)
- Follow-up TODOs: None
-->

# Constitución del Proyecto: Módulo ERP de Inventario (pyme, solo frontend)

## Core Principles

### I. Interfaz 100% en Español
Todo el texto visible para el usuario —etiquetas, botones, mensajes de validación y error, estados vacíos, toasts, ayuda y documentación en pantalla— DEBE estar en español (es-CL para formatos de fecha, moneda y números). No se aceptan cadenas en inglés en la interfaz; el código fuente y los identificadores técnicos pueden permanecer en inglés. Cualquier texto nuevo se revisa antes de dar por terminada la historia.

### II. Persistencia Exclusiva en localStorage
La aplicación es solo frontend con Vite + JavaScript vanilla sobre el template; NO existe backend. Todo dato de dominio (productos, movimientos, configuración de módulos, campos personalizados) DEBE persistirse en `localStorage` a través de la capa de almacenamiento (`src/storage.js`), nunca en variables de memoria efímeras ni en servicios remotos. El esquema de almacenamiento debe ser versionado y tolerante a migraciones simples; no se introduce ninguna dependencia de red para datos de negocio.

### III. Pruebas con Vitest antes de Cerrar una Historia (NON-NEGOTIABLE)
Ninguna historia se considera terminada si sus pruebas Vitest no existen y pasan. El comportamiento de lógica (storage, validaciones, cálculos de stock) se cubre con pruebas unitarias en `tests/unit/`; los flujos de usuario (crear/editar/eliminar entidades, documentos, dashboard, búsqueda) se cubren con pruebas de integración en `tests/integration/` siguiendo el patrón existente del repositorio. Las pruebas se escriben antes o junto con la implementación, y se verifica además que no existan regresiones en las pruebas previas.

### IV. Accesibilidad Básica
Toda la interfaz DEBE cumplir un mínimo de accesibilidad: HTML semántico, navegación completa por teclado, foco visible y orden lógico, etiquetas asociadas a controles de formulario, contraste suficiente, atributos `aria-*` donde el HTML nativo no basta, y estados de error/vacío anunciados de forma comprensible. La accesibilidad se verifica en la revisión de cada historia que toque la interfaz, no como tarea aparte al final.

### V. Cuidado de Datos Sensibles y Sesgos
Aunque los datos viven en localStorage, el módulo trata información de negocio de una pyme (costos, proveedores, personas). Se DEBE: (a) no exponer datos sensibles en logs, consola ni mensajes de error; (b) nunca enviar datos a servicios externos; (c) usar datos de ejemplo ficticios y no estereotipados en demostraciones y pruebas; (d) evitar sesgos en nomenclatura, ejemplos y casos de uso (nombres, roles, géneros) representando la diversidad real de una pyme. Cualquier riesgo detectado se registra y se mitiga antes del cierre de la historia.

### VI. Trazabilidad de Decisiones en GitHub Issues
Toda decisión relevante —cambios de alcance, alternativas descartadas, trade-offs técnicos, deudas aceptadas, riesgos o supuestos nuevos— DEBE registrarse como Issue en GitHub con contexto, alternativas consideradas y justificación. Las decisiones menores no requieren Issue, pero sí deben quedar reflejadas en el plan o la especificación. Una historia solo se cierra si sus decisiones relevantes están trazadas.

## Restricciones de Proyecto
- Stack fijo: Vite + JavaScript vanilla (sin frameworks de UI ni state management externo) sobre el template base del repositorio.
- Sin backend ni llamadas de red para datos de negocio; persistencia únicamente vía localStorage (Principio II).
- Herramienta de pruebas: Vitest (ya configurado en `vitest.config.mjs`); no se introducen otros frameworks de prueba.
- El módulo debe seguir siendo extensible: la configuración de módulos (`src/module-config.js`) permite agregar módulos futuros del ERP (p. ej. ventas, compras) sin reescribir el shell.

## Flujo de Trabajo por Historias
Cada historia sigue el ciclo: especificar → planificar → implementar con pruebas → verificar cumplimiento de esta constitución → registrar Issues de decisiones relevantes → cerrar solo cuando las pruebas Vitest pasan y la interfaz cumple los Principios I y IV. El incumplimiento de cualquier principio debe bloquear el cierre de la historia.

## Governance
Esta constitución prevalece sobre cualquier práctica ad-hoc del proyecto. Las enmiendas requieren justificación documentada, actualización de las plantillas y planes afectados, y un Issue en GitHub que registre el cambio. El cumplimiento se revisa durante la planificación, la revisión de implementación y antes del cierre de cada historia; las desviaciones DEBEN justificarse explícitamente y quedar trazadas.

**Version**: 1.0.0 | **Ratified**: 2026-11-14 | **Last Amended**: 2026-11-14
