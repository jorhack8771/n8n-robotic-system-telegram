# n8n-robotic-system-telegram
<img width="862" height="346" alt="image" src="https://github.com/user-attachments/assets/549cb5fb-8c68-4de3-90b4-0b47a0d924d8" />

{
  "name": "My workflow",
  "nodes": [
    {
      "parameters": {
        "content": "BotFather\n[TOKEN ELIMINADO]\n\n",
        "height": 80,
        "width": 304,
        "color": 6
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -336,
        -48
      ],
      "typeVersion": 1,
      "id": "09980bb0-2c27-41b4-8e0f-55812b47e1ac",
      "name": "Sticky Note"
    },
    {
      "parameters": {
        "content": "Prompt (User Message)\n{{ $json.message.text }}",
        "height": 80,
        "width": 256,
        "color": 6
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        272,
        -128
      ],
      "typeVersion": 1,
      "id": "9ab9a811-7cec-4d18-83eb-2c0803413a0c",
      "name": "Sticky Note1"
    },
    {
      "parameters": {
        "updates": [
          "message"
        ],
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegramTrigger",
      "typeVersion": 1.3,
      "position": [
        0,
        0
      ],
      "id": "251a7cab-5a42-4241-bbc5-31de268ea69c",
      "name": "Telegram Trigger",
      "webhookId": "6d18a3e3-60a5-46cf-95e6-be0696bc882d",
      "credentials": {
        "telegramApi": {
          "id": "[ID ELIMINADO]",
          "name": "Telegram account"
        }
      }
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "=",
        "options": {
          "systemMessage": "System Message Optimizado\n\"Actúa como un Asistente de Ventas y Atención al Cliente amable, eficiente y profesional. Tu objetivo es ayudar a los clientes consultando información y agendando citas.\n\nTus Herramientas de Trabajo:\n\nGoogle Sheets: Úsala obligatoriamente para verificar precios, disponibilidad o detalles de productos antes de responder. No inventes información.\n\nGoogle Calendar: Úsala exclusivamente para registrar citas confirmadas.\n\nTus Reglas de Operación:\n\nConsulta de Información: Ante dudas de precios o productos, consulta Google Sheets. Si el producto no aparece, di amablemente que no tienes información actualizada y ofrece ayuda con otro producto.\n\nGestión de Citas (Agendamiento):\n\nSi el cliente desea agendar, extrae: Nombre completo, Servicio, Fecha y Hora.\n\nSi falta algún dato, solicítalo con calidez (ej: '¡Claro, [Nombre]! Para terminar de agendar, ¿me confirmas a qué hora te gustaría asistir?').\n\nUna vez que tengas los 4 datos, utiliza la herramienta Google Calendar para crear el evento.\n\nConfirmación: Después de usar Google Calendar, confirma al cliente: '¡Listo! Tu cita para [Servicio] ha quedado agendada para el [Fecha] a las [Hora]. ¡Te esperamos!'.\n\nAtención al Cliente: Mantén un tono profesional, servicial y humano. Sé conciso pero amable.\n\nLimitaciones: Si el usuario solicita algo que no puedes resolver, dirígelo a un representante humano de forma natural.\n\nFormato: Usa emojis de forma moderada para que la conversación sea cercana.\"\n"
        }
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3.1,
      "position": [
        208,
        0
      ],
      "id": "1aa6067b-593d-4228-96cf-151eff1d8b4d",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "model": "openai/gpt-oss-20b",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGroq",
      "typeVersion": 1,
      "position": [
        80,
        208
      ],
      "id": "9befa618-0531-41fb-81e5-dfc0651a6b66",
      "name": "Groq Chat Model",
      "credentials": {
        "groqApi": {
          "id": "[ID ELIMINADO]",
          "name": "Groq account"
        }
      }
    },
    {
      "parameters": {
        "sessionIdType": "customKey",
        "sessionKey": "={{ $workflow }}",
        "contextWindowLength": 10
      },
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.4,
      "position": [
        224,
        208
      ],
      "id": "9694b1c1-6dfc-4c4a-b791-4dc949582ed7",
      "name": "Simple Memory"
    },
    {
      "parameters": {
        "descriptionType": "manual",
        "toolDescription": "Get row(s) in sheet in Google Sheets",
        "documentId": {
          "__rl": true,
          "value": "https://docs.google.com/spreadsheets/d/13_PFdQ8K-jImqXwjLWFGsKjgQUxIDdfnNdCEbsl7JqA/edit?gid=0#gid=0",
          "mode": "url"
        },
        "sheetName": {
          "__rl": true,
          "value": "Hoja 1",
          "mode": "name"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheetsTool",
      "typeVersion": 4.7,
      "position": [
        368,
        208
      ],
      "id": "a77ad240-fc65-4484-9570-3c82b82ba16c",
      "name": "Get row(s) in sheet in Google Sheets",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "[ID ELIMINADO]",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "chatId": "={{ $('Telegram Trigger').item.json.message.chat.id }}",
        "text": "={{ $json.output }}",
        "replyMarkup": "=none",
        "forceReply": {},
        "replyKeyboardOptions": {},
        "replyKeyboardRemove": {},
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        560,
        0
      ],
      "id": "5c183e01-9a2a-4e7f-94f1-f91670fef9e0",
      "name": "Send a text message",
      "webhookId": "26044ca6-04e4-4082-bb94-1f2ea99e7ad9",
      "credentials": {
        "telegramApi": {
          "id": "[ID ELIMINADO]",
          "name": "Telegram account"
        }
      }
    },
    {
      "parameters": {
        "content": "promt AI asistente \nActúa como un Asistente de Atención al Cliente y Ventas altamente eficiente. Tu objetivo es proporcionar información precisa, resolver dudas y gestionar citas utilizando la base de datos de Google Sheets.\n\nTus Reglas de Operación:\n\nConsulta de Información: Ante cualquier consulta sobre precios o productos, utiliza siempre la herramienta 'Get row(s) in sheet in Google Sheets' para verificar el dato real antes de responder. No inventes precios ni existencias.\n\nGestión de Citas (Agendamiento): Si el usuario desea agendar una cita, extrae: Nombre, Servicio, Fecha y Hora. Si falta algún dato, solicítalo amablemente. Una vez completos, usa la herramienta de Google Sheets para registrar la cita.\n\nAtención al Cliente: Mantén un tono profesional, amable y servicial. Responde de forma concisa.\n\nLimitaciones: Si el usuario pide algo fuera de tus capacidades, dirígelo amablemente a un representante humano.\n\nFormato: Utiliza emojis de forma moderada.",
        "height": 288,
        "width": 496
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -400,
        -368
      ],
      "typeVersion": 1,
      "id": "3de0f814-7150-439f-84ee-a922abe5bc19",
      "name": "Sticky Note2"
    },
    {
      "parameters": {
        "descriptionType": "manual",
        "toolDescription": "Create an event in Google Calendar\"Utiliza esta herramienta para crear una cita en Google Calendar. Requiere obligatoriamente tres parámetros: 'start' (fecha y hora de inicio, formato ISO), 'end' (fecha y hora de finalización, formato ISO, por defecto 1 hora después del inicio) y 'summary' (descripción del evento, incluyendo nombre del cliente y servicio).\"",
        "calendar": {
          "__rl": true,
          "value": "family01064798720974439626@group.calendar.google.com",
          "mode": "list",
          "cachedResultName": "Familia"
        },
        "start": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('Start', ``, 'string') }}",
        "end": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('End', ``, 'string') }}",
        "useDefaultReminders": "={{ $fromAI('Use_Default_Reminders', ``, 'boolean') }}",
        "additionalFields": {
          "summary": "={{ /*n8n-auto-generated-fromAI-override*/ $fromAI('Summary', ``, 'string') }}"
        }
      },
      "type": "n8n-nodes-base.googleCalendarTool",
      "typeVersion": 1.3,
      "position": [
        544,
        240
      ],
      "id": "5d9fb736-0f23-4779-bfdd-52e07690e266",
      "name": "Create an event in Google Calendar",
      "credentials": {
        "googleCalendarOAuth2Api": {
          "id": "[ID ELIMINADO]",
          "name": "Google Calendar account"
        }
      }
    }
  ],
  "connections": {
    "Telegram Trigger": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Groq Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Simple Memory": {
      "ai_memory": [
        [
          {
            "node": "AI Agent",
            "type": "ai_memory",
            "index": 0
          }
        ]
      ]
    },
    "Get row(s) in sheet in Google Sheets": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    },
    "AI Agent": {
      "main": [
        [
          {
            "node": "Send a text message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Create an event in Google Calendar": {
      "ai_tool": [
        [
          {
            "node": "AI Agent",
            "type": "ai_tool",
            "index": 0
          }
        ]
      ]
    }
  }
}
```[cite: 1]


