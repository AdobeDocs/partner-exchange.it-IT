---
title: Importazione in tempo reale
description: Scopri come importare i dati in AEP in tempo reale.
exl-id: 0b6215a9-1160-49ae-8aa5-302b47357200
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# Trasmetti dati ad AEP

Adobe [!DNL Experience Platform] consente lo streaming e la disponibilità in tempo reale degli eventi di profilo e di esperienza. Tutti i dati inviati ad AEP tramite streaming vengono mantenuti nel data lake. I dati possono essere inviati in streaming a set di dati esistenti o completamente nuovi tramite API o utilizzando Adobe Launch.

Il presente articolo riguarda:

* Streaming al profilo individuale XDM
* Streaming a XDM ExperienceEvent
* Utilizzo di AEP per lo streaming dell’estensione Launch

Il [Raccolta Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) viene inserito un riferimento in tutto l’articolo utilizzando le chiamate associate per numero. Maggiori dettagli sull’installazione e l’utilizzo della raccolta Postman sono disponibili su Github [LEGGIMI](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) pagina. Sono inoltre disponibili set di dati di esempio di [fedeltà](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) e [profilo](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) dati.

## Prerequisiti

* [Autenticazione sulla piattaforma](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html).
* Raccogli i valori per le intestazioni richieste dal tutorial sull’autenticazione collegato in precedenza.

## Creare una connessione in streaming

Per inviare in streaming ad AEP devi prima creare una connessione in streaming. Le connessioni in streaming contengono attributi come l’origine dei dati in streaming e specificano se si inviano o meno record che appartengono al [!DNL Experience Data Model] (XDM). Dopo aver creato una connessione in streaming, riceverai un URL univoco da utilizzare per lo streaming dei dati in AEP.

Vai [qui](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection.html) per istruzioni su come creare una connessione in streaming tramite API o [qui](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection-ui.html) per istruzioni su come creare una connessione in streaming tramite l’interfaccia utente.

```json
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

Risposta:

```json
 {
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

Assicurati di salvare l’ID fornito nella risposta precedente per le chiamate di acquisizione in streaming future (la raccolta Postman lo salverà automaticamente nella variabile di ambiente CONNECTION_ID).

## Trasmetti dati profilo ad AEP

Per questa sezione, utilizza le cartelle di chiamate di Postman: 3: importazione in tempo reale, 3a: importazione in tempo reale per i dati di PROFILO.

Sono documentate richieste JSON dettagliate con risposte per i dati del profilo di streaming [qui](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-record-data.html).

Passaggi:

1. Creare uno schema profilo individuale XDM
1. Impostare il descrittore di identità primaria per il profilo individuale XDM (chiave primaria)
1. Creare un set di dati per i singoli record profilo XDM
1. Chiama le API Streaming Ingestion per creare un record XDM per profilo individuale
1. Recupera il nuovo profilo creato

## Trasmetti eventi esperienza ad AEP

Per questa sezione, utilizza le cartelle di chiamate di Postman: 3: importazione in tempo reale, 3b: importazione in tempo reale per i dati di PROFILO.

Sono documentate le richieste JSON dettagliate con le risposte per i dati sull’esperienza di streaming [qui](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-time-series-data.html).

Passaggi:

1. Creare uno schema XDM ExperienceEvent
1. Impostare il descrittore di identità primaria per ExperienceEvent XDM (chiave primaria)
1. Creare un set di dati per ExperienceEvents XDM
1. Chiama le API Streaming Ingestion per creare un ExperienceEvent XDM
1. Recupera il nuovo evento creato

## Utilizza i tag di Experience Platform per inviare in streaming ad AEP

L’Adobe [!DNL Experience Platform] L&#39;estensione Launch consente di eseguire lo streaming su AEP tramite Launch. Per ulteriori informazioni, consulta [questa guida](https://docs.adobe.com/content/help/it-IT/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html).

## Articoli di riferimento

* [API di acquisizione dati](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [Panoramica sull’acquisizione in streaming](https://docs.adobe.com/content/help/it-IT/experience-platform/ingestion/home.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/streaming_ingest_overview.md)
* [Guida per gli sviluppatori sull’acquisizione in streaming](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/getting_started_with_platform_streaming_ingestion.md)
* [Utilizzo dell&#39;estensione AEP Launch](https://docs.adobe.com/content/help/it-IT/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)
