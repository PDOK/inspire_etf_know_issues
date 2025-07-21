# Know issues

Deze repo bevat een lijst van alle onderkende validatie fouten uit de automatische etf validatie. Per type validatie fout kan  informatie toegevoegd worden, om een oplossing(srichting) te beschrijven of om te verwijzen naar reeds aangemaakt tickets (intern bij pdok, of extern biuj het [Inspire MIF](https://github.com/INSPIRE-MIF/helpdesk-validator/issues))

Telkens als er een automatische etf validatie draait wordt de inhoud van csv in deze repo in de ETF database geladen en worden known issues middels queries in het [etf validatie grafana dashboard](https://pdok.cloud.kadaster.nl/grafana/d/fL3ApY1Gk/etf-validatie?orgId=1) gekoppeld aan de validatiefouten.

---
### Known issue 

- **status** 

  geeft aan bij wie dit ticket belegt is. Mogelijk te gebruiken waarden zijn: 
  - **BU** (Business)
  - **BU_ACCEPTED** (Door de Business geaccepteerde fout / won't fix)
  - **IT** (IT, Actie voor IT om verder te analyseren, in veel gevallen bevat de omschrijving een hint naar een mogelijk oplossing)
  - **EU** (Er is een ticket aanmaakt bij de [inspire helpdesk validator](https://github.com/INSPIRE-MIF/helpdesk-validator/issues))

- **link** 
  
  url naar een gerelateerd Jira ticket of een ticket van de [inspire helpdesk validator](https://github.com/INSPIRE-MIF/helpdesk-validator/issues)

- **omschrijving**

  Hier kan een omschijving opgenomen worden die beschrijft wat en waarom iets fout gaat, of er kan een oplosrichting opgegeven worden


---
### Hoe te linken aan validatie fouten

Om een onderkende validatie fouten te linken aan een hierboven beschreven oplossing of ticket, dienen 1 of meerdere van onderstaande velden ingevuld te worden in de csv file. Zo kan gelinkt worden aan een specifieke assertion met mogelijke een specifieke foutmelding. Hoe gelinkt wordt is afhankelijk van welke velden ingevuld worden. Als een veld niet ingevuld wordt er niet op dit veld gefilterd.

- **test_suite_id** (optioneel) TODO

  Het id van de testsuite. we kennen (momenteel) de volgende testsuites:
  | Testsuite                               | id                                      |
  |-----------------------------------------|-----------------------------------------|
  | ATOM service                            | EID11571c92-3940-4f42-a6cd-5e2b1c6f4d93 |
  | WMS service                             | EIDeec9d674-d94b-4d8d-b744-1309c6cae1d2 |
  | WFS service                             | EID174edf55-699b-446c-968c-1892a4d8d5bd |
  | WCS service                             | EID074570ad-d720-47b3-af79-d54201793404 |
  | WMTS service                            | EID550ceacf-b3cb-47a0-b2dd-d3edb18344a9 |
  | OGC API service                         | EIDc543e1ad-465d-3162-ac1a-badef588dc76 |
  | Common metadata                         | EID59692c11-df86-49ad-be7f-94a1e1ddd8da |
  | Dataset metadata                        | EID2be1480a-fe42-40b2-9420-eb0e69385c80 |
  | Dataset metadata for monitoring         | EID0b86f7a3-2947-4841-823d-6a00d8e06d70 | 
  | Netwerk service metadata                | EID606587df-65a8-4b7b-9eee-e0d94daaa42a |
  | Netwerk service metadata for monitoring | EIDb0e0e8dd-68f8-461e-9090-d6fad9418cdb |
  | SDS Invocable metadata                  | EID8db54d8a-8578-4959-b891-5394d9f53a28 |
  | SDS Interoperable metadata              | EID7514777a-6cb8-499c-acd5-912496dc84e9 |
  | SDS Harmonised metadata                 | EIDa593a7ad-42d9-46d0-985d-9dff3e684428 |

- **test_step_id** (optioneel)

  Id van de test stap

- **test_assertion_id**

  Id van de test assertion

- **error_message**

  Type foutmelding (bv 'TR.missingElement')

- **error_message_contains**

  WIP! hier kan gefilterd worden op een specifieke string die in de foutmelding voor komt.

- **metadata_uuids**

  Een lijst van service metadata id om een know issue te koppelen aan 1 of meerdere services. De lijst wordt omsloten met curly braces ({}) en verschillende uuids moeten gescheiden worden met commas. dus bv `{uuid1}` of `{uuid1,uuid2}`

Om te gebruiken is te achterhalen kan het beste de te downloaden csv met alle validatiefouten opgehaald worden in [grafana](https://pdok.cloud.kadaster.nl/grafana/d/fL3ApY1Gk/etf-validatie?orgId=1) (zie *Download csv* rechtsboven in het dashboard).

LetOp!
- Het grafana dashboard geeft geen inzicht of een gekoppeld Jira ticket nog open of reeds gesloten is. Het is daarom noodzakelijk om regelmatig te kijken of er gelinkt is naar gesloten tickets. Dit kan voorkomen als reeds opgeloste fouten later weer terugkomen of omdat nieuwe services eenzelfde fout kunnen veroorzaken.
- Het kan voorkomen dat een fout door verschillende combinaties in de filtering gekoppeld wordt aan meerdere know issues. In dat geval komt de fout meerdere keren voor op het grafan dashboard (in de telling wordt deze fout dan niet dubbel geteld)