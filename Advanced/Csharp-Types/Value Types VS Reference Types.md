In C# zijn er twee soorten typen: value types en reference types.

Value types zijn typen die hun waarde opslaan in hun eigen geheugenruimte. Dit betekent dat de variabelen van deze typen de waarden direct bevatten. Voorbeelden van value types zijn `int`, `float`, `bool`, `struct`, en `enum`. Value types worden op de stack opgeslagen.

Reference types zijn typen die een verwijzing naar een object in het geheugen bevatten. Dit betekent dat de variabelen van deze typen een referentie naar de locatie van het object bevatten. Voorbeelden van reference types zijn `string`, `object`, `class`, en `delegate`. Reference types worden op de heap opgeslagen.

Value types worden meestal gebruikt voor eenvoudige gegevensstructuren die klein zijn en weinig overhead hebben. Reference types worden meestal gebruikt voor complexe objecten die groter zijn en meer overhead hebben.

Het belangrijkste verschil tussen value types en reference types is hoe ze worden opgeslagen in het geheugen en hoe ze worden doorgegeven tussen methoden. Value types worden doorgegeven als kopieën, terwijl reference types worden doorgegeven als referenties.