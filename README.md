# n8n-robotic-system-telegram
<img width="862" height="346" alt="image" src="https://github.com/user-attachments/assets/549cb5fb-8c68-4de3-90b4-0b47a0d924d8" />

# Asistente de Ventas con n8n y Telegram

Bot de automatización para atención al cliente y gestión de citas.

## 🚀 Características
- **Atención 24/7**: Respuesta automática a clientes vía Telegram.
- **Consulta Inteligente**: Verifica precios y productos directamente en Google Sheets.
- **Gestión de Citas**: Agenda eventos automáticamente en Google Calendar.

## 🛠 Cómo instalarlo
1. Descarga el archivo `my_workflow.json` de la carpeta `/workflows`.
2. En tu instancia de n8n, ve a **Workflows** > **Import from file...**.
3. Selecciona el archivo descargado.
4. Configura tus propias credenciales en los nodos correspondientes:
   - Telegram API
   - Groq API
   - Google Sheets API
   - Google Calendar API

## 📋 Requisitos
- Una instancia de n8n activa.
- Cuentas configuradas en Telegram, Google Cloud (para Sheets/Calendar) y Groq.
