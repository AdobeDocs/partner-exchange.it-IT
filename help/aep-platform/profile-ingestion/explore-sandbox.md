---
title: Accedere ed esplorare la sandbox di AEP
description: Scopri come accedere ed esplorare la sandbox di Experience Platform.
exl-id: 62c21615-4b03-4900-a1ad-8f809c836491
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# Accedere ed esplorare la sandbox di AEP

Il presente articolo riguarda:

* Differenze tra un’organizzazione sandbox Adobe Exchange Partner esistente e la sandbox AEP condivisa.
* Richiesta di accesso alla sandbox condivisa di AEP.
* Ricezione di un invito e-mail alla sandbox condivisa di AEP.
* Invitare nuovi utenti in [!DNL Admin Console].
* Navigazione nell’interfaccia utente di AEP.

Per una panoramica generale della tecnologia Sandbox in AEP, consulta [articolo](https://docs.adobe.com/content/help/en/experience-platform/sandbox/home.html).

## Sandbox AEP condivisa

I partner di Exchange hanno accesso a vari Adobi [!DNL Experience Cloud] prodotti (prodotti non AEP come [!DNL Analytics], [!DNL Target], tag Platform e così via) tramite il proprio Adobe [!DNL Experience Cloud] Organizzazione (non condivisa). Ai partner vengono concessi i diritti di accesso come amministratore di sistema alla propria organizzazione per gestire gli utenti e altre autorizzazioni. Adobe [!DNL Experience Platform] (AEP) viene trattato in modo diverso rispetto ad altre sandbox di Adobe. Di seguito sono riportate le principali differenze:

* L&#39;accesso ad AEP NON avverrà tramite l&#39;Adobe principale dei partner [!DNL Experience Cloud] organizzazione sandbox.
* L&#39;accesso ad AEP avviene tramite un&#39;organizzazione di Exchange Adobe condivisa.
* Molte altre aziende partner di Adobe Exchange accedono ad AEP utilizzando la stessa organizzazione
   * Tramite la funzione Sandbox AEP, i dati e le attività all’interno di questa organizzazione condivisa non possono essere visualizzati o modificati dagli altri partner; ogni partner avrà accesso a una sandbox diversa all’interno dell’organizzazione condivisa.
* I diritti di amministrazione all’interno di questa organizzazione condivisa sono molto limitati.
* Dopo aver ottenuto l’accesso a una sandbox su AEP, i partner visualizzeranno due organizzazioni nello switcher dell’organizzazione in alto a destra nell’interfaccia utente, nella pagina principale dell’Admin Console o dell’Experience Cloud principale. Tuttavia, una volta effettuato l’accesso ad AEP, dovrebbe essere visibile solo l’organizzazione condivisa.

## Richiedi accesso alla sandbox AEP condivisa

Invia un [richiesta di supporto](https://adobeexchangeec.zendesk.com/hc/it-it/requests/new) con le seguenti informazioni:

* Indirizzo e-mail
* Oggetto: Richiesta Sandbox AEP
* Prodotto: Provisioning generale/Sandbox
* Tipo di ticket: Supporto per il programma - Programma di scambio / Domande sulla richiesta di provisioning
* Descrizione: fornisci una breve descrizione dei casi di utilizzo dell’integrazione che richiedono l’utilizzo di una sandbox AEP
* Assicurati anche di fornire tutti i nomi utente e le e-mail che devono essere aggiunti alla sandbox di AEP. È possibile aggiungere altri utenti dopo aver effettuato la richiesta, ma gli utenti dovranno essere aggiunti per Adobe tramite un ticket aggiuntivo (vedi di seguito).

## Ricevi l’invito e-mail

Il contatto principale che ha richiesto la sandbox di AEP riceverà un’e-mail automatizzata con l’invito a &quot;iniziare&quot; a utilizzare l’Adobe [!DNL Experience Platform]. Il contatto principale disporrà inoltre di alcuni privilegi di amministrazione descritti nella sezione successiva.

Invece di selezionare il pulsante &quot;Inizia&quot; nell’e-mail, accedi direttamente a `https://platform.adobe.com.` Accedi con l’Adobe ID associato all’indirizzo e-mail nell’invito oppure creane uno se non è associato a un Adobe ID.

## Invita altri utenti

Invia un [richiesta di supporto](https://adobeexchangeec.zendesk.com/hc/it-it/requests/new) con le seguenti informazioni:

* Indirizzo e-mail del richiedente
* Oggetto: Sandbox AEP - Aggiungi amministratore/utente
* Prodotto: Provisioning generale/Sandbox
* Tipo di ticket: Supporto per il programma - Programma di scambio / Domande sulla richiesta di provisioning
* Descrizione: elenco di utenti da aggiungere (nomi e indirizzi e-mail)

## Navigazione nell’interfaccia utente di AEP

Guarda l’interfaccia utente di AEP [video introduttivo](https://docs.adobe.com/content/help/en/platform-learn/tutorials/intro-to-platform/interface-tour.html)

Nell’interfaccia utente di AEP sono disponibili 12 aree principali in cui è possibile effettuare la navigazione tramite il pannello a sinistra. Tuttavia, le sezioni più importanti per questo tipo di integrazione sono Schemi, Set di dati e Profili.

* Home - la schermata di destinazione

   * Suggerisce alcune attività iniziali
   * Fornisce alcuni collegamenti ai contenuti di apprendimento
   * Offre una visualizzazione dashboard per alcuni degli oggetti AEP principali, ad esempio Schemi, Set di dati e Profili

* Flussi di lavoro: introduzione nei flussi di lavoro comuni per l’inserimento di dati in AEP
* Connessioni/origini: gestisci le origini dei dati in arrivo in AEP
* Connessioni/Destinazioni: gestisci le connessioni per l’invio dei dati a sistemi esterni
* Profili: visualizzare e gestire i profili dei singoli clienti
* Segmenti: sfogliare, creare e modificare i segmenti dei clienti
* Identità: sfoglia, crea e modifica gli spazi dei nomi delle identità; si tratta dei tipi di ID primari utilizzati per identificare in modo univoco un cliente
* Modelli (Data Science): partecipare ad attività di Data Science, incluso l’utilizzo di un ambiente Jupyter Notebooks incorporato
* Servizi (Data Science): pubblicare ricette di data science come servizi
* Schemi: per sfogliare, creare e modificare gli schemi, ovvero le definizioni di dati dettagliate utilizzate per mantenere organizzati i dati
* Set di dati: consente di sfogliare, creare e gestire i set di dati. Un set di dati è definito da uno schema ed è il punto in cui i dati risiedono in AEP
* Query: consente di sfogliare, creare, modificare e utilizzare un archivio di query per ottenere informazioni dai dati all’interno di DataSet
* Monitoraggio: visualizza lo stato di tutti i dati in entrata e in uscita da AEP, sia per batch che per streaming
