---
title: Importare dati batch in AEP
description: Scopri come importare file batch in Experienci Platform
exl-id: 50576b67-b3ba-498e-86f6-7e1986b76985
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Importare dati batch in AEP

AEP può acquisire file batch che contengono dati di profilo da un file flat (come parquet) o dati conformi a uno schema noto in [!UICONTROL Experience Data Model] (XDM).

AEP può acquisire dati utilizzando file batch. Sono accettati i seguenti formati: JSON, Parquet e CSV.

Il presente articolo riguarda:

* Prerequisiti per l’acquisizione in batch
* Best practice e limiti per l’acquisizione in batch
* Come creare un batch
* Come completare un batch
* Controllare lo stato di un batch

Il [Raccolta Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) viene inserito un riferimento in tutto l’articolo utilizzando le chiamate associate per numero. Maggiori dettagli sull’installazione e l’utilizzo della raccolta Postman sono disponibili su Github [LEGGIMI](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) pagina. Sono inoltre disponibili set di dati di esempio di [fedeltà](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) e [profilo](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) dati.

Per tutte le chiamate di questa esercitazione, utilizza le cartelle di chiamate di Postman: 4: Importazione batch, 4a: Importazione batch per i dati PROFILO OPPURE 4b: Importazione batch per i dati EVENTO.

## Prerequisiti per l’acquisizione in batch

* Definisci uno schema e crea un set di dati.
* I dati devono essere formattati in JSON, Parquet o CSV.
* [Autenticazione sulla piattaforma](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md).
* Raccogli i valori per le intestazioni richieste dal tutorial sull’autenticazione collegato in precedenza.

## Best practice e limiti per l’acquisizione in batch

* Dimensione massima batch: 100 GB
* Numero massimo di file per batch: 1500
* Se un file supera i 512 MB, deve essere diviso in blocchi più piccoli. Ulteriori dettagli sono disponibili nella sezione [guida per sviluppatori](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* Numero massimo di proprietà o campi per riga: 10.000
* Numero massimo di batch al minuto per utente: 138

## Creare un batch

In questo tutorial utilizzeremo JSON come formato. Altri esempi di formati sono disponibili nella [guida per sviluppatori](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
Crea un batch utilizzando JSON come formato di input (assicurati di includere un ID set di dati e che i dati siano conformi allo schema XDM collegato al set di dati):

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
  -d '{
          "datasetId": "{DATASET_ID}",
           "inputFormat": {
                "format": "json"
           }
      }'
```

Risposta:

```json
{
    "id": "{BATCH_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 0,
    "status": "loading",
    "created": 0,
    "relatedObjects": [
        {
            "type": "dataSet",
            "id": "{DATASET_ID}"
        }
    ],
    "version": "1.0.0",
    "tags": {},
    "createdUser": "{USER_ID}",
    "updatedUser": "{USER_ID}"
}
```

## Carica file

Ora è possibile caricare i file nel batch appena creato (utilizzando batch_id dalla risposta precedente).

```json
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/datasets/{DATASET_ID}/files/{FILE_NAME}.json" \
  -H "content-type: application/octet-stream" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  --data-binary "@{FILE_PATH_AND_NAME}.json"
```

>[!NOTE]
>
>L’API supporta solo il caricamento in una sola parte, il che significa che ogni file/micro-batch dovrà essere caricato con singole chiamate. Assicurati che il tipo di contenuto sia application/octet-stream.

Risposta:

```
200 OK
```

## Completare un batch

Una volta caricati tutti i file, questa chiamata segnalerà che il batch è pronto per la promozione:

```json
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Risposta:

```
200 OK
```

## Controllare lo stato di un batch

Lo stato del batch può essere controllato nell’interfaccia utente o tramite l’API (vedi chiamata di seguito). Per archiviare l’interfaccia utente, passa a DataSet per visualizzare lo stato.

È possibile trovare i vari stati di acquisizione batch [qui](https://adobe.ly/2TMMCmj).


```json
curl GET "https://platform.adobe.io/data/foundation/catalog/batch/{BATCH_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Risposta:

```json
{
    "{BATCH_ID}": {
        "imsOrg": "{IMS_ORG}",
        "created": 1494349962314,
        "createdClient": "MCDPCatalogService",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "updated": 1494349963467,
        "externalId": "{EXTERNAL_ID}",
        "status": "success",
        "errors": [
            {
                "code": "err-1494349963436"
            }
        ],
        "version": "1.0.3",
        "availableDates": {
            "startDate": 1337,
            "endDate": 4000
        },
        "relatedObjects": [
            {
                "type": "batch",
                "id": "foo_batch"
            },
            {
                "type": "connection",
                "id": "foo_connection"
            },
            {
                "type": "connector",
                "id": "foo_connector"
            },
            {
                "type": "dataSet",
                "id": "foo_dataSet"
            },
            {
                "type": "dataSetView",
                "id": "foo_dataSetView"
            },
            {
                "type": "dataSetFile",
                "id": "foo_dataSetFile"
            },
            {
                "type": "expressionBlock",
                "id": "foo_expressionBlock"
            },
            {
                "type": "service",
                "id": "foo_service"
            },
            {
                "type": "serviceDefinition",
                "id": "foo_serviceDefinition"
            }
        ],
        "metrics": {
            "foo": 1337
        },
        "tags": {
            "foo_bar": [
                "stuff"
            ],
            "bar_foo": [
                "woo",
                "baz"
            ],
            "foo/bar/foo-bar": [
                "weehaw",
                "wee:haw"
            ]
        },
        "inputFormat": {
            "format": "parquet",
            "delimiter": ".",
            "quote": "`",
            "escape": "\\",
            "nullMarker": "",
            "header": "true",
            "charset": "UTF-8"
        }
    }
}
```

## Articoli di riferimento

* [API di acquisizione dati](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Panoramica dell’acquisizione in batch](https://docs.adobe.com/content/help/it-IT/experience-platform/ingestion/home.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/ingest_architectural_overview.md)
* [Guida per gli sviluppatori sull’acquisizione in batch](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_developer_guide.md)
* [Guida alla risoluzione dei problemi di acquisizione in batch](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/ingest_architectural_overview/batch_data_ingestion_troubleshooting_guide.md)
* [Raccolta Postman per l’acquisizione dei dati](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Data%20Ingestion%20API.postman_collection.json)
* [Tutorial sull’autenticazione](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)
