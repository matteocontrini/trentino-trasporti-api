# Trentino Trasporti API

Reverse engineering delle API dell'app Muoversi in Trentino. Include i ritardi in tempo reale dei mezzi.

- Base URL: `https://app-tpl.tndigit.it/gtlservice`
- Autenticazione: `Basic`
  - Username: `mittmobile`
  - Password: `ecGsp.RHB3`
- Header (opzionali):
  - `User-Agent` della web view dello smartphone
  - `X-Requested-With: it.tndigit.mit`

## Lista fermate

- Endpoint: `GET /stops`
- Query string:
  - `size`: limite sul numero di risultati. Default: tutti. (opzionale)
  - `type`: filtro sul tipo di fermata. (opzionale)
    - `U` per urbano (inclusa funivia)
    - `E` per extraurbano (inclusa ferrovia)
- Struttura risposta: array di fermate
- Esempio fermata urbana:
```json
{
    "distance": null,
    "routes": [
        {
            "areaId": 0,
            "news": null,
            "routeColor": "BF6092",
            "routeId": 466,
            "routeLongName": "P.Dante Rosmini S.Rocco Povo Polo Soc.",
            "routeShortName": "13",
            "routeType": 3,
            "type": "U"
        },
        {
            "areaId": 0,
            "news": null,
            "routeColor": null,
            "routeId": 535,
            "routeLongName": "P.Dante P.Fiera Università Mesiano Povo",
            "routeShortName": "5/",
            "routeType": 3,
            "type": "U"
        }
    ],
    "stopCode": "25055z",
    "stopDesc": "",
    "stopId": 2683,
    "stopLat": 46.067773,
    "stopLevel": 60,
    "stopLon": 11.150538,
    "stopName": "Povo Polo Scientifico Est",
    "street": "Via Sommarive",
    "town": "Trento",
    "type": "U",
    "wheelchairBoarding": 2
}
```
- Esempio fermata extraurbana:
```json
{
    "distance": null,
    "routes": [
        {
            "areaId": 0,
            "news": null,
            "routeColor": null,
            "routeId": 691,
            "routeLongName": "Trento-Bassano Trentino Trasporti Spa",
            "routeShortName": "R25",
            "routeType": 2,
            "type": "E"
        },
        {
            "areaId": 0,
            "news": null,
            "routeColor": null,
            "routeId": 693,
            "routeLongName": "Trento-Borgo Trentino Trasporti Spa",
            "routeShortName": "R26",
            "routeType": 2,
            "type": "E"
        },
        {
            "areaId": 0,
            "news": null,
            "routeColor": null,
            "routeId": 695,
            "routeLongName": "Servizi Trenitalia - Andata Tn-Bassano",
            "routeShortName": "R25",
            "routeType": 2,
            "type": "E"
        }
    ],
    "stopCode": "4449FS",
    "stopDesc": "",
    "stopId": 5149,
    "stopLat": 46.051416,
    "stopLevel": 60,
    "stopLon": 11.514744,
    "stopName": "Strigno-Staz. Fs",
    "street": "Strada Statale 47 della Valsugana",
    "town": "Villa Agnedo",
    "type": "E",
    "wheelchairBoarding": 0
}
```

## Lista linee

- Endpoint: `GET /routes`
- Query string:
  - `areas`: filtro sul tipo di linea. Anche valori multipli, separati da virgola. Default: tutte. (opzionale)
    - Urbano:
      - `23` per Trento
      - `24` per Rovereto
      - `22` per l'Alto Garda
      - `21` per Pergine Valsugana
    - Extraurbano: `1`, `2`, `3`, `4`, `5`, `6` per i rispettivi bacini
    - Ferrovia: `7` 
    - Funivia: `8`
- Struttura risposta: array di linee
- Esempio linea urbana:
```json
{
    "areaId": 23,
    "news": [],
    "routeColor": "BABAB7",
    "routeId": 614,
    "routeLongName": "P.Dante Ospedale Fersina Clarina P.Dante",
    "routeShortName": "A",
    "routeType": 3,
    "type": "U"
}
```
- Esempio linea urbana (con avviso modifica orari):
```json
{
    "areaId": 23,
    "news": [
        {
            "agencyId": "12",
            "details": "Con decorrenza lunedi' 09 gennaio 2023 vengono modificati gli orari delle corse della linea 5 limitate a POVO \"Polo Sociale\" nella fascia oraria 16.00 - 19.00",
            "endDate": "/Date(1673654400)/",
            "header": "S.U. TRENTO - MODIFICA ORARI CORSE LINEA 5",
            "idFeed": null,
            "routeIds": [
                400
            ],
            "serviceType": "Urbano Trento",
            "startDate": "/Date(1672704000)/",
            "stopId": "",
            "url": "https://www.trentinotrasporti.it/avvisi/8737-s-u-trento-modifica-orari-corse-linea-5-2023-9"
        }
    ],
    "routeColor": "F5C500",
    "routeId": 400,
    "routeLongName": "Piazza Dante P.Fiera Povo Oltrecastello",
    "routeShortName": "5",
    "routeType": 3,
    "type": "U"
}
```
- Esempio linea urbana con colore assente:
```json
{
    "areaId": 23,
    "news": [],
    "routeColor": null,
    "routeId": 612,
    "routeLongName": "04 Lavis Zona Industriale Lavis",
    "routeShortName": "L4",
    "routeType": 3,
    "type": "U"
}
```
- Esempio linea extraurbana:
```json
{
    "areaId": 1,
    "news": [],
    "routeColor": null,
    "routeId": 300,
    "routeLongName": "Pergine - Civezzano",
    "routeShortName": "B115",
    "routeType": 3,
    "type": "E"
}
```
- Esempio linea extraurbana (con avviso):
```json
{
    "areaId": 1,
    "news": [
        {
            "agencyId": "12",
            "details": "Con decorrenza immediata sono temporaneamente sospese le fermate di Lago di Tesero e di Masi \"Az.Agricola\" e Masi via Miceletti.",
            "endDate": "/Date(1686355200)/",
            "header": "Sospensione ferrmate a Masi e Lago di Tesero",
            "idFeed": null,
            "routeIds": [
                1,
                136
            ],
            "serviceType": "Extraurbano provinciale",
            "startDate": "/Date(1650412800)/",
            "stopId": "",
            "url": "https://www.trentinotrasporti.it/avvisi/7923-sospensione-ferrmate-a-masi-e-lago-di-tesero-2022-204"
        }
    ],
    "routeColor": null,
    "routeId": 1,
    "routeLongName": "Cavalese-Predazzo-Moena-Canazei-Penia",
    "routeShortName": "B101",
    "routeType": 3,
    "type": "E"
}
```
- Esempio ferrovia:
```json
{
    "areaId": 7,
    "news": [],
    "routeColor": null,
    "routeId": 352,
    "routeLongName": " FERROVIA TRENTO - MALE' - MEZZANA",
    "routeShortName": "R35",
    "routeType": 2,
    "type": "E"
}
```
- Esempio ferrovia (con avvisi):
```json
{
    "areaId": 7,
    "news": [
        {
            "agencyId": "12",
            "details": "Si informa la gentile clientela che l'orario sulla linea ferroviaria Trento - Borgo - Bassano viene riprogrammato con validita' da domenica 8 gennaio a domenica 12 febbraio 2023. I servizi effettuati con treno sono evidenziati in giallo nell'orario allegato.",
            "endDate": "/Date(1676160000)/",
            "header": " Linea ferroviaria R25-R26 TRENTO - BORGO - BASSANO: orario dall'8 gennaio al 12 febbraio 2023",
            "idFeed": null,
            "routeIds": [
                691,
                693,
                695
            ],
            "serviceType": "Ferrovia",
            "startDate": "/Date(1671667200)/",
            "stopId": "",
            "url": "https://www.trentinotrasporti.it/avvisi/8716-linea-ferroviaria-r25-r26-trento-borgo-bassano-orario-dall-8-gennaio-al-12-febbraio-2023-2022-891"
        }
    ],
    "routeColor": null,
    "routeId": 691,
    "routeLongName": "Trento-Bassano Trentino Trasporti Spa",
    "routeShortName": "R25",
    "routeType": 2,
    "type": "E"
}
```
- Funivia:
```json
{
    "areaId": 8,
    "news": [],
    "routeColor": null,
    "routeId": 531,
    "routeLongName": "Funivia Trento Sardagna",
    "routeShortName": "Fu",
    "routeType": 5,
    "type": "U"
}
```

## Lista corse

- Endpoint: `GET /trips_new`
- Query string:
  - Corse per una linea:
    - `routeId`: ID della linea. (obbligatorio)
    - `type`: tipo di corsa, `U` per urbano, `E` per extraurbano. (obbligatorio)
    - `limit`: numero di corse da ritornare. Ritorna sempre il doppio di quelle richieste. (obbligatorio)
    - `directionId`: filtro sulla direzione, `0` per andata e `1` per ritorno. (opzionale)
    - `refDateTime`: orario di passaggio/partenza per il quale si richiedono le corse. Formato ISO 8601 (es. `2023-01-14T13:14:00Z`). (opzionale)
  - Corse per una fermata:
    - `stopId`: ID della fermata. (obbligatorio)
    - `type`: vedi sopra. (obbligatorio)
    - `limit`: numero di corse da ritornare. (obbligatorio)
    - `refDateTime`: vedi sopra. (opzionale)
- Struttura risposta: array di corse
- Esempio corsa per una linea:
```json5
{
    "cableway": null,
    "corsaPiuVicinaADataRiferimento": false,
    "delay": 6.0,
    "directionId": 0,
    "indiceCorsaInLista": 45,
    "lastEventRecivedAt": "2023-01-13T11:12:48Z",
    "lastSequenceDetection": 15,
    "matricolaBus": 310,
    "oraArrivoEffettivaAFermataSelezionata": null,
    "oraArrivoProgrammataAFermataSelezionata": null,
    "routeId": 400,
    "stopLast": 183,
    "stopNext": 186,
    "stopTimes": [
        {
            "arrivalTime": "11:49:00",
            "departureTime": "11:49:00",
            "stopId": 247,
            "stopSequence": 1,
            "tripId": "0003790302022091220230609",
            "type": "U"
        },
        {
            "arrivalTime": "11:51:00",
            "departureTime": "11:51:00",
            "stopId": 407,
            "stopSequence": 2,
            "tripId": "0003790302022091220230609",
            "type": "U"
        },
        {
            "arrivalTime": "11:53:00",
            "departureTime": "11:53:00",
            "stopId": 444,
            "stopSequence": 3,
            "tripId": "0003790302022091220230609",
            "type": "U"
        },
        // ...omitted...
        {
            "arrivalTime": "12:13:00",
            "departureTime": "12:13:00",
            "stopId": 161,
            "stopSequence": 23,
            "tripId": "0003790302022091220230609",
            "type": "U"
        }
    ],
    "totaleCorseInLista": 136,
    "tripFlag": "TRIP_FLAG__MID",
    "tripHeadsign": "Oltrecastello",
    "tripId": "0003790302022091220230609",
    "type": "U",
    "wheelchairAccessible": 1
}
```
- Esempio di corsa per una fermata:
```json5
{
    "cableway": null,
    "corsaPiuVicinaADataRiferimento": false,
    "delay": null,
    "directionId": 1,
    "indiceCorsaInLista": 0,
    "lastEventRecivedAt": null,
    "lastSequenceDetection": 0,
    "matricolaBus": null,
    "oraArrivoEffettivaAFermataSelezionata": "2023-01-13T11:17:00Z",
    "oraArrivoProgrammataAFermataSelezionata": "2023-01-13T11:17:00Z",
    "routeId": 536,
    "stopLast": 0,
    "stopNext": 0,
    "stopTimes": [
        {
            "arrivalTime": "12:16:00",
            "departureTime": "12:16:00",
            "stopId": 235,
            "stopSequence": 1,
            "tripId": "0003804452022091220230609",
            "type": "U"
        },
        {
            "arrivalTime": "12:17:00",
            "departureTime": "12:17:00",
            "stopId": 231,
            "stopSequence": 2,
            "tripId": "0003804452022091220230609",
            "type": "U"
        },
        // ...omitted...
        {
            "arrivalTime": "12:44:00",
            "departureTime": "12:44:00",
            "stopId": 284,
            "stopSequence": 19,
            "tripId": "0003804452022091220230609",
            "type": "U"
        }
    ],
    "totaleCorseInLista": 0,
    "tripFlag": "TRIP_FLAG__START",
    "tripHeadsign": "Bolghera \"S.Antonio\"",
    "tripId": "0003804452022091220230609",
    "type": "U",
    "wheelchairAccessible": 1
}
```

## Corsa singola

- Endpoint: `GET /trips/{tripId}`
- Struttura risposta: singola corsa (vedi in "Lista corse")

## Bike sharing

- Endpoint: `GET /poi/bikesharing`
- Struttura risposta: array di postazioni bike sharing
- Esempio:
```json5
[
    {
        "address": "Via Grazioli / P.za Venezia",
        "bikes": 3,
        "id": "Piazza Venezia - Trento",
        "name": "Piazza Venezia",
        "position": [
            46.06753791402558,
            11.126987115869156
        ],
        "slots": 21,
        "totalSlots": 24
    },
    // ...
]
```

## Altro

- `GET /poi/contextaware/stazioni`: qualcosa legato all'accessibilità delle stazioni.
- `GET /direction?from=46.060280,11.125581&lang=it&to=46.066130,11.152206`: indicazioni stradali. La struttura è quasi la stessa delle Directions API di Google.

