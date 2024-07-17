---
title: "[!DNL Platform] Panoramica della guida all'acquisizione del profilo e all'integrazione degli accessi"
description: Scopri l'integrazione per l'acquisizione e l'accesso al profilo  [!DNL Experience Platform] .
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%

---

# Guida all&#39;integrazione: acquisizione e accesso al profilo [!DNL Experience Platform]

I partner devono utilizzare questa guida all&#39;integrazione per aiutarli a creare funzionalità di ingresso e uscita con Adobe [!DNL Experience Platform] (AEP). Sono disponibili API per l’acquisizione batch, l’acquisizione in streaming e l’accesso al profilo unificato (in uscita).

Per assistenza nello sviluppo, il team Adobe Exchange ha creato una [raccolta Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman). Viene fatto riferimento a questa raccolta Postman in tutta la guida all’integrazione.

Ulteriori dettagli sull&#39;installazione e l&#39;utilizzo della raccolta Postman sono disponibili nella pagina Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md). Sono inoltre presenti set di dati di esempio di [dati fedeltà](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) e [profilo](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json).

## Esempio di utilizzo dell’integrazione: sistema di risposta vocale interattiva

Per gli integratori, le API [!DNL Experience Platform] forniscono tutte le funzionalità della piattaforma offerte in tutta l&#39;interfaccia utente, ma ora possono creare flussi di lavoro cliente e flussi di dati automatizzati. In qualità di integratore, puoi controllare periodicamente lo stato dei set di dati, impostare nuove procedure di acquisizione dei dati e integrare la tua soluzione di attivazione del pubblico con Unified Profile.

Si consideri il mondo dei sistemi di risposta vocale interattiva (IVR) e del software di gestione del call center. Il fornitore può utilizzare le API [!DNL Experience Platform] per acquisire informazioni cronologiche sull&#39;attività del call center del cliente nel data lake dell&#39;esperienza. Se i dati vengono acquisiti nello schema XDM `ExperienceEvent` (uno schema che esprime le interazioni dei clienti), queste interazioni possono essere acquisite senza attrito direttamente nel servizio Unified Profile. In questo caso, `callerId` viene utilizzato come identificatore del cliente. Il servizio Identity si occuperà della risoluzione delle identità e assisterà il servizio Unified Profile nell’aggiungere al profilo del cliente tutti i punti dati derivanti da interazioni recenti con il call center.

La prossima volta che un cliente chiama il Call Center, riceve una risposta dall’IVR. Per personalizzare il messaggio e consegnare un&#39;offerta personalizzata per il chiamante, il sistema IVR deve conoscere meglio il chiamante. Qui entra in gioco l’integrazione API con Unified Profile. Il backend IVR può contattare il servizio Unified Profile per una ricerca di punti. Quindi, consulta gli attributi del profilo che si applicano solo alle interazioni del call center o il profilo cliente completo, che ha anche gli attributi per le interazioni su altri punti di contatto. Combinando dati provenienti da più origini dati, utilizzando la risoluzione delle identità, e il profilo unificato, il call center e il provider IVR possono offrire un&#39;esperienza personalizzata al cliente, supportata dall&#39;Adobe [!DNL Experience Platform].&quot;

## Risorse generali

* AEP [Documentazione del prodotto](https://docs.adobe.com/content/help/en/experience-platform/landing/documentation/overview.html).
* AEP [Estensibilità](https://www.adobe.com/insights/experience-platform-api-extensibility.html).

## Domande o feedback?

Invia tutte le domande e il feedback tramite il [canale di supporto](https://adobeexchangeec.zendesk.com/hc/it-it/requests/new)
