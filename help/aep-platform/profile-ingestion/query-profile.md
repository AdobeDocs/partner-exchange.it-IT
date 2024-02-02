---
title: Accedere al profilo unificato
description: Utilizza le API per accedere al profilo unificato.
exl-id: c9d2fa2d-9ffe-4e66-996f-ad930bee22c6
source-git-commit: fe7519c35fb9155ce54cad85941c887f15881a38
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Accedere al profilo unificato utilizzando l’API del profilo

L’Adobe [!DNL Experience Platform] può accedere al profilo cliente in tempo reale; il [[!DNL Experience Platform] API Profilo cliente in tempo reale](https://adobe.ly/2TtDHWr) è stato progettato per interagire con esso. Vedi questo [esercitazione](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html) per informazioni su come accedere ai dati del profilo cliente in tempo reale utilizzando l’API di profilo.

Questo articolo farà riferimento in modo sostanziale all’esercitazione collegata in precedenza.

Il [Raccolta Postman](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman) viene inserito un riferimento in tutto l’articolo utilizzando le chiamate associate per numero. Maggiori dettagli sull’installazione e l’utilizzo della raccolta Postman sono disponibili su Github [LEGGIMI](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) pagina. Sono inoltre disponibili set di dati di esempio di [fedeltà](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) e [profilo](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) dati.

Per questa sezione, utilizza la cartella Postman 5: Ricerca profilo, 5a: Dati profilo di ricerca in tempo reale OPPURE 5b: Dati EVENTO di ricerca in tempo reale.

## Mediante l’API

Le sezioni seguenti sono utili per l’autenticazione in Experienci Platform. Scopri il percorso API, le informazioni sull’intestazione e altro ancora.

### Autentica in [!DNL Platform]

Consulta [questo](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html) tutorial di autenticazione prima di effettuare una delle chiamate di seguito.

### Percorso API

L’URL del gateway della piattaforma necessario per l’API del profilo cliente in tempo reale è: `https://platform.adobe.io/`

Il percorso di base per l’API è: `/data/core/ups/access/entities`

Un esempio di percorso completo è: `https://platform.adobe.io/data/core/ups/access/entities`

### Informazioni intestazione

L’intestazione deve includere:

* Authorization
* x-gw-ims-org-id - da ottenere tramite console.adobe.io
* x-api-key: da ottenere tramite console.adobe.io
* x-sandbox-name - ottenuto da Adobe Integration Manager
* Content-Type: application/json

Ulteriori informazioni sull’intestazione sono disponibili nella sezione [esercitazione](https://adobe.ly/2PTHuKv).

## Accesso ai profili cliente in tempo reale tramite identità

L’API di profilo consente di accedere ai profili utilizzando un’identità tramite una richiesta GET. Le sezioni seguenti seguiranno questo [guida](https://docs.adobe.com/content/help/en/experience-platform/profile/api/entities.html).

### Accedere ai dati del profilo utilizzando l’identità

L’API consente di accedere alle informazioni del profilo utilizzando l’identità. A tal fine, effettua una richiesta GET a /access/entities con l’ID entità come uno dei parametri e uno degli ID ID spazio dei nomi dell’entità. NOTA: qualsiasi richiesta che restituisca 50 record restituirà solo lo stato HTTP 422 e un messaggio con la dicitura &quot;troppe identità correlate&quot;. La ricerca dovrà essere limitata con più parametri.

Richiesta:

La richiesta seguente recupera l’e-mail e il nome di un cliente utilizzando un’identità:

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Risposta:

```
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

### Accedere ai profili per elenco di identità

L’API consente di accedere ai profili utilizzando un elenco di identità tramite una richiesta POST all’endpoint /access/entities e fornendo le identità nel payload. Queste identità sono costituite da un valore ID (entityId) e da uno spazio dei nomi delle identità (entityIdNS).

Richiesta: la seguente richiesta recupera i nomi e gli indirizzi e-mail di diversi clienti da un elenco di identità:

```
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema":{
        "name":"_xdm.context.profile"
    },
    "fields":["identities","person.name","workEmail"],
    "identities":[
        {
            "entityId":"89149270342662559642753730269986316601",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316900",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316602",
            "entityIdNS":{
                "code":"ECID"
            }
        }
    ]
}'
```

Risposta: in caso di esito positivo, la risposta restituisce i campi richiesti delle entità specificate nel corpo della richiesta.

```
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## Eventi di serie temporali

I partner possono accedere agli eventi della serie temporale in base all’identità dell’entità profilo associata, effettuando una richiesta GET all’endpoint /access/entities.

### Accedere agli eventi di serie temporali per un profilo in base all’identità

L’identità dell’entità profilo associata accede agli eventi della serie temporale effettuando una richiesta GET all’endpoint /access/entities. Questa identità è costituita da un valore ID (entityId) e da uno spazio dei nomi delle identità (entityIdNS).

Richiesta: la richiesta seguente trova un’entità profilo per ID e recupera i valori per le proprietà endUserIDs, web e channel **per tutti** eventi di serie temporali associati all’entità.

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Risposta:

In caso di esito positivo, la risposta restituisce un elenco impaginato di eventi di serie temporali e dei campi associati specificati nei parametri di richiesta.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### Impaginazione per eventi di serie temporali per un profilo

I risultati vengono impaginati durante il recupero degli eventi delle serie temporali. Se sono presenti pagine successive di risultati, il parametro _page.next della risposta conterrà un ID. Inoltre, il parametro _links.next.href della risposta fornisce un URI di richiesta per recuperare la pagina successiva.

Richiesta:

La richiesta seguente recupera la pagina successiva dei risultati utilizzando l’URI _links.next.href come percorso della richiesta.

```
curl -X GET \

  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

Risposta:

In caso di esito positivo, la risposta restituisce la pagina successiva di risultati. In questo esempio viene illustrata una risposta in cui non sono presenti pagine successive di risultati, come indicato dai valori stringa vuoti _page.next e _links.next.href.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## Articoli di riferimento

* [API Profilo cliente in tempo reale](https://adobe.ly/2TtDHWr)
* [Accedere ai dati del profilo cliente in tempo reale utilizzando l’esercitazione API profilo](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html)
* [[!DNL Experience Platform] Guida all’autenticazione](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)
