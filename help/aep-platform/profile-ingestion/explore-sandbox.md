---
title: Accedere ed esplorare la sandbox di AEP
description: Scopri come accedere ed esplorare la sandbox di Experience Platform.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
TQID: https://experienceleague.adobe.com/A5sl-xNZBPjIKn6HO1iwM78IaQWQs4yBgbw9wwpMrGw
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
feature_v2:
  - id: fdbb8fc9-ffa3-4b86-88fe-aa4c5a3e1bc6
subfeature_v2:
  - id: b75843fa-0a67-4a44-a6b1-cc627b0481dc
  - id: fef08361-6ac5-460c-93fe-d063e40b6a49
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 772
ht-degree: 1%

---

# Accedere ed esplorare la sandbox di AEP

Il presente articolo riguarda:

* Le differenze tra un’organizzazione sandbox partner Adobe Exchange esistente e la sandbox AEP condivisa.
* Richiesta di accesso alla sandbox condivisa di AEP.
* Ricezione di un invito e-mail alla sandbox condivisa di AEP.
* Invito di nuovi utenti in [!DNL Admin Console].
* Navigazione nell’interfaccia utente di AEP.

Per una panoramica generale della tecnologia Sandbox in AEP, consulta questo [articolo](https://docs.adobe.com/content/help/it-IT/experience-platform/sandbox/home.html).

## Sandbox AEP condivisa

I partner di Exchange possono accedere a vari prodotti Adobe [!DNL Experience Cloud] (prodotti non AEP come [!DNL Analytics], [!DNL Target], tag Platform e così via) tramite la propria organizzazione Adobe [!DNL Experience Cloud] (non condivisa). Ai partner vengono concessi i diritti di accesso come amministratore di sistema alla propria organizzazione per gestire gli utenti e altre autorizzazioni. Adobe [!DNL Experience Platform] (AEP) viene trattato in modo diverso rispetto alle altre sandbox di Adobe. Di seguito sono riportate le principali differenze:

* L&#39;accesso ad AEP NON avverrà tramite l&#39;organizzazione sandbox principale di Adobe [!DNL Experience Cloud] dei partner.
* L’accesso ad AEP avviene tramite un’organizzazione Adobe Exchange condivisa.
* Molte altre aziende partner di Adobe Exchange accedono ad AEP utilizzando la stessa organizzazione
   * Con la funzione Sandbox di AEP, i dati e le attività all’interno di questa organizzazione condivisa non possono essere visti o modificati dagli altri partner; ogni partner avrà accesso a una sandbox diversa all’interno dell’organizzazione condivisa.
* I diritti di amministrazione all’interno di questa organizzazione condivisa sono molto limitati.
* Dopo aver ottenuto l’accesso a una sandbox su AEP, i partner visualizzeranno due organizzazioni nello switcher dell’organizzazione in alto a destra nell’interfaccia utente, nella pagina Home di Admin Console o Experience Cloud principale. Tuttavia, una volta effettuato l’accesso ad AEP, dovrebbe essere visibile solo l’organizzazione condivisa.

## Richiedere l’accesso alla sandbox di AEP condivisa

Invia una [richiesta di supporto](https://adobeexchangeec.zendesk.com/hc/it-it/requests/new) con le seguenti informazioni:

* Indirizzo e-mail
* Oggetto: Richiesta Sandbox AEP
* Prodotto: Provisioning generale/Sandbox
* Tipo di ticket: Supporto per il programma - Programma di scambio / Domande sulla richiesta di provisioning
* Descrizione: fornisci una breve descrizione dei casi di utilizzo dell’integrazione che richiedono l’utilizzo di una sandbox di AEP
* Assicurati anche di fornire tutti i nomi utente e le e-mail che devono essere aggiunti alla sandbox di AEP. È possibile aggiungere altri utenti dopo che la richiesta è stata effettuata, ma gli utenti dovranno essere aggiunti da Adobe tramite un ticket aggiuntivo (vedi di seguito).

## Ricevi l’invito e-mail

Il contatto principale che ha richiesto la sandbox di AEP riceverà un&#39;e-mail automatica con l&#39;invito a &quot;iniziare&quot; a utilizzare Adobe [!DNL Experience Platform]. Il contatto principale disporrà inoltre di alcuni privilegi di amministrazione descritti nella sezione successiva.

Invece di selezionare il pulsante &quot;Inizia&quot; nell&#39;e-mail, passa direttamente a `https://platform.adobe.com.` Accedi con l&#39;Adobe ID associato all&#39;indirizzo e-mail nell&#39;invito oppure creane uno se non è associato a un Adobe ID.

## Invita altri utenti

Invia una [richiesta di supporto](https://adobeexchangeec.zendesk.com/hc/it-it/requests/new) con le seguenti informazioni:

* Indirizzo e-mail del richiedente
* Oggetto: Sandbox AEP - Aggiungi amministratore/utente
* Prodotto: Provisioning generale/Sandbox
* Tipo di ticket: Supporto per il programma - Programma di scambio / Domande sulla richiesta di provisioning
* Descrizione: elenco di utenti da aggiungere (nomi e indirizzi e-mail)

## Navigazione nell’interfaccia utente di AEP

Guarda il video introduttivo [sull&#39;interfaccia utente di AEP](https://docs.adobe.com/content/help/it-IT/platform-learn/tutorials/intro-to-platform/interface-tour.html)

Nell’interfaccia utente di AEP sono disponibili 12 aree principali in cui è possibile spostarsi tramite il pannello a sinistra. Tuttavia, le sezioni più importanti per questo tipo di integrazione sono Schemi, Set di dati e Profili.

* Home - la schermata di destinazione

   * Suggerisce alcune attività iniziali
   * Fornisce alcuni collegamenti ai contenuti di apprendimento
   * Offre una visualizzazione dashboard per alcuni dei principali oggetti di AEP, ad esempio Schemi, Set di dati e Profili

* Flussi di lavoro: introduzione nei flussi di lavoro comuni per l’inserimento di dati in AEP
* Connessioni/origini: gestire le origini dei dati in AEP
* Connessioni/Destinazioni: gestisci le connessioni per l’invio dei dati a sistemi esterni
* Profili: visualizzare e gestire i profili dei singoli clienti
* Segmenti: sfogliare, creare e modificare i segmenti dei clienti
* Identità: sfoglia, crea e modifica gli spazi dei nomi delle identità; si tratta dei tipi di ID primari utilizzati per identificare in modo univoco un cliente
* Modelli (Data Science): partecipare ad attività di Data Science, incluso l’utilizzo di un ambiente Jupyter Notebooks incorporato
* Servizi (Data Science): pubblicare ricette di data science come servizi
* Schemi: per sfogliare, creare e modificare gli schemi, ovvero le definizioni di dati dettagliate utilizzate per mantenere organizzati i dati
* Set di dati: consente di sfogliare, creare e gestire i set di dati; un set di dati è definito da uno schema ed è il punto in cui i dati risiedono in AEP
* Query: consente di sfogliare, creare, modificare e utilizzare un archivio di query per ottenere informazioni dai dati all’interno di DataSet
* Monitoraggio: visualizza lo stato di tutti i dati in entrata e in uscita da AEP, sia per batch che per streaming
