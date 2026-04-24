# Laboratorio 2: Implementación de Seguridad Móvil en Flutter

## Introducción
Este proyecto implementa controles de seguridad críticos para aplicaciones financieras, enfocándose en la protección de las comunicaciones y el almacenamiento seguro de credenciales.

## Objetivos
1. Implementar Certificate Pinning para prevenir ataques Man-in-the-Middle (MitM).
2. Asegurar el almacenamiento de tokens de sesión utilizando Hardware-backed storage.
3. Centralizar el manejo de excepciones de seguridad en la capa de red.

## Arquitectura de Seguridad
El proyecto utiliza una estructura por capas para separar la lógica de negocio de la infraestructura de red:

- **lib/network/api_client.dart**: Configuración de Dio y SecurityContext para la validación estricta de certificados.
- **lib/network/token_interceptor.dart**: Interceptor para la gestión automatizada de cabeceras de autorización.
- **lib/network/security_error_handler.dart**: Traductor de excepciones técnicas a mensajes de usuario seguros.
- **lib/network/flutter_secure_storage**: Integración con Keychain (iOS) y Keystore (Android).

## Requisitos Previos
- Flutter SDK >= 3.10.0
- Certificado del servidor en formato PEM en `assets/certs/server_cert.pem`.

## Instalación
1. Clonar el repositorio.
2. Ejecutar `flutter pub get`.
3. Configurar el host local o mock server para `api.bancasegura.test`.

## Pruebas de Seguridad (Checkpoints)
1. **Checkpoint 1 (Conexión Exitosa)**: Se valida que el cliente acepta conexiones únicamente cuando el certificado coincide con el pin local.
2. **Checkpoint 2 (Error de Certificado)**: Se verifica que el HandshakeException es capturado y notificado correctamente al usuario cuando el certificado es inválido o expirado.
3. **Checkpoint 3 (Header Authorization)**: Validación en logs de la inclusión correcta del Bearer token en cada petición saliente.
