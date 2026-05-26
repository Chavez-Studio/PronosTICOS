# PronosTICOS
Aplicación para quiniela del mundial 2026

🏆 PronósTICOS - Mundial 2026 Quiniela

PronósTICOS es una aplicación web progresiva (PWA) diseñada para gestionar una quiniela (juego de pronósticos deportivos) enfocada en la Copa Mundial de la FIFA 2026. Está construida con una arquitectura Serverless utilizando React en el frontend y Google Apps Script (GAS) junto con Google Sheets como backend y base de datos.

Desarrollado por C-Studio © 2026.

✨ Características Principales

📱 Para los Usuarios

Autenticación Segura: Registro e inicio de sesión con encriptación de contraseñas (Hash SHA-256) del lado del cliente.

Pronósticos Base: Interfaz intuitiva para ingresar predicciones de marcadores. Guardado automático tras dejar de escribir.

Predicciones Extra: En partidos seleccionados, los usuarios pueden predecir:

Primer Anotador / Goleador

MVP del partido

Minuto de un gol (con margen de error de $\pm 1$ minuto)

Bloqueo Automático: Los pronósticos se bloquean por seguridad exactamente 1 hora antes del inicio programado de cada partido.

Ranking Dinámico: Tabla de posiciones global en tiempo real con desglose detallado de estadísticas por usuario e historial de predicciones.

Fase de Grupos: Tablas de posiciones reales de los equipos automatizadas según los resultados de los partidos.

PWA (Progressive Web App): Instalable en la pantalla de inicio de iOS y Android como una aplicación nativa.

🛡️ Para los Administradores (Modo Dios)

Gestión de Partidos: Actualización del estado de los partidos (PROGRAMADO, EN VIVO, FINALIZADO).

Ingreso de Resultados: Carga de marcadores reales y valores de predicciones extra (Goleadores, MVP, Minutos).

Control de Usuarios: Capacidad para forzar el cambio de contraseña de usuarios que hayan olvidado sus credenciales.

Habilitar Extras: Control manual para decidir qué partidos llevarán predicciones adicionales.

⚙️ Tecnologías Utilizadas

Frontend: React.js 18 (Standalone via Babel), Tailwind CSS, FontAwesome.

Backend: Google Apps Script (Node.js/V8 engine).

Base de Datos: Google Sheets.

Seguridad: API Web Crypto (SHA-256) nativa del navegador.

📊 Sistema de Puntuación

El motor de puntuación evalúa las predicciones de la siguiente manera (Máximo 10 puntos por partido):

Puntos Base (Excluyentes)

6 Puntos (Marcador Exacto): Acierto del ganador y la cantidad exacta de goles de ambos equipos.

4 Puntos (Tendencia Correcta): Acierto del ganador + diferencia de goles, acertar un empate no exacto, o acertar los goles exactos de un solo equipo.

3 Puntos (Solo Ganador): Acierto de qué equipo ganó, fallando en el resto de variables.

Puntos Extra (Acumulativos)

(Solo aplicables si el administrador habilitó extras para el partido)

+1 Punto (Primer Anotador): El jugador elegido anotó al menos un gol (excluye autogoles y tandas de penales).

+1 Punto (MVP): Acierto exacto del Jugador del Partido oficial.

+2 Puntos (Minuto del Gol): Adivinar el minuto de cualquier gol del partido, con un margen de tolerancia de $\pm 1$ minuto.

🗄️ Estructura de la Base de Datos (Google Sheets)

Para que el sistema funcione correctamente, el libro de Google Sheets debe contener las siguientes hojas con su estructura de columnas:

1. usuarios

| id (UUID) | username | email | password (Hash) | timestamp | isAdmin (TRUE/FALSE) |

2. equipos

| id (Ej: EQ01) | nombre | codigo (Ej: MEX) | grupo | img (URL bandera) | emoji |

3. jugadores

| id | equipo_id (Debe coincidir con el código o ID de equipos) | nombre |

4. partidos

| id | localId | visitaId | fecha (ISO) | estadio | ciudad | etapa | realLocal | realVisita | status | tieneExtras (SI/NO) | rGol | rMvp | rMin |

5. pronosticos

| id_compuesto (userId_matchId) | userId | matchId | predLocal | predVisita | ptsTotales | timestamp | pGol | pMvp | pMin |

🚀 Despliegue y Configuración

Crear un proyecto en Google Apps Script asociado a una hoja de cálculo de Google.

Copiar el código del Backend al archivo Code.gs.

Crear un archivo HTML llamado index_pwa.html y pegar el código del Frontend.

Poblar las hojas de cálculo con los equipos, jugadores y calendario de partidos.

Hacer clic en Implementar > Nueva Implementación como "Aplicación Web".

Ejecutar como: Yo

Quién tiene acceso: Cualquier persona

Autorizar los permisos requeridos por el script (Lectura de Sheets y envío de correos mediante MailApp).

Distribuir la URL generada a los jugadores.
