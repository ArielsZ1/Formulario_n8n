# Trabajo Práctico: Integración de MIT App Inventor, n8n y Google Sheets

Este repositorio contiene la resolución del trabajo práctico que demuestra la integración de una aplicación móvil desarrollada en **MIT App Inventor** con Google Sheets, utilizando la plataforma de automatización **n8n** y Cuentas de Servicio de Google Cloud.

## Documentación del Proceso

---

## Evidencia de Ejecución

A continuación se comprueba el correcto funcionamiento del flujo de datos, desde la aplicación móvil, pasando por el Webhook, hasta la escritura final en la hoja de cálculo:

### 1. Lógica de envío en MIT App Inventor (JSON Request)
![image alt](https://github.com/ArielsZ1/Formulario_n8n/blob/main/UI.jpeg)

### 2. Datos almacenados correctamente en Google Sheets
![image alt](https://github.com/ArielsZ1/Formulario_n8n/blob/main/GoogleSheets.jpeg)


### 3. Flujo ejecutado con éxito en n8n
![image alt](https://github.com/ArielsZ1/Formulario_n8n/blob/main/n8n.jpeg)

---

## Flujo exportado de n8n (JSON)

A continuación, se adjunta el código fuente del flujo de automatización (Webhook + Google Sheets) listo para ser importado en cualquier instancia de n8n.

<details>
<summary>Haz clic aquí para desplegar el código JSON</summary>

```json
{
  "name": "My workflow",
  "nodes": [
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "formulario-app",
        "options": {
          "allowedOrigins": "*"
        }
      },
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2.1,
      "position": [
        0,
        0
      ],
      "id": "bdcf224c-098d-46e8-8090-764451ec73d9",
      "name": "Webhook",
      "webhookId": "76f36919-14cf-492b-b4b2-49edfecef0db"
    },
    {
      "parameters": {
        "operation": "appendOrUpdate",
        "documentId": {
          "__rl": true,
          "value": "1p_zrvhjoQ2w1QnAsNdy-leAMgn8WOpsXKzJgl03aDRY",
          "mode": "list",
          "cachedResultName": "Documento",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1p_zrvhjoQ2w1QnAsNdy-leAMgn8WOpsXKzJgl03aDRY/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Hoja 1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1p_zrvhjoQ2w1QnAsNdy-leAMgn8WOpsXKzJgl03aDRY/edit#gid=0"
        },
        "columns": {
          "mappingMode": "defineBelow",
          "value": {
            "Nombre": "={{ $json.body.nombre }}",
            "Apellido ": "={{ $json.body.apellido }}",
            "Estado": "={{ $json.body.estado }}",
            "Observaciones ": "={{ $json.body.observaciones }}",
            "Fecha": "={{ $json.body.fecha }}"
          },
          "matchingColumns": [
            "Nombre"
          ],
          "schema": [
            {
              "id": "Nombre",
              "displayName": "Nombre",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Apellido ",
              "displayName": "Apellido ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Estado",
              "displayName": "Estado",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Observaciones ",
              "displayName": "Observaciones ",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            },
            {
              "id": "Fecha",
              "displayName": "Fecha",
              "required": false,
              "defaultMatch": false,
              "display": true,
              "type": "string",
              "canBeUsedToMatch": true,
              "removed": false
            }
          ],
          "attemptToConvertTypes": false,
          "convertFieldsToString": false
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        208,
        0
      ],
      "id": "dbcc2691-e0ed-4cf2-bc02-a5b4e070da2e",
      "name": "Append or update row in sheet",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "kiEMYdke6sJnnarE",
          "name": "Google Sheets OAuth2 API"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "Webhook": {
      "main": [
        [
          {
            "node": "Append or update row in sheet",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": true,
  "settings": {
    "executionOrder": "v1",
    "binaryMode": "separate",
    "availableInMCP": false,
    "timeSavedMode": "fixed",
    "callerPolicy": "workflowsFromSameOwner"
  },
  "versionId": "4275004c-d615-4eef-8e40-ea0174f02413",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "e8469ed75dd1d36dd5797936bc310357fe499d9f5e1f9269b747b3a194dd4800"
  },
  "nodeGroups": [],
  "id": "O7Qc13r7ue0TINF4",
  "tags": []
}
