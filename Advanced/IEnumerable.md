[[yield in IEnumerable]] <-- dit gaat over de yield return statement.
`IEnumerable` en `List` zijn beide datatypes in C# die worden gebruikt om verzamelingen van items op te slaan, maar ze verschillen in functionaliteit en gebruik.

### IEnumerable:

- `IEnumerable` is een interface die collecties van items vertegenwoordigt die kunnen worden geïtereerd (doorlopen) met behulp van een `foreach`-lus.
- Het is de meest fundamentele vorm van iteratie over een verzameling en biedt alleen de mogelijkheid om items één voor één te doorlopen, maar niet om elementen toe te voegen of te verwijderen.
- Het biedt basisfunctionaliteiten voor het doorlopen van een verzameling, zoals `MoveNext()` om naar het volgende element te gaan, `Current` om het huidige element op te halen, en `GetEnumerator()` om een enumerator te verkrijgen.
- `IEnumerable` wordt veel gebruikt voor lazy evaluation (uitgestelde evaluatie), wat betekent dat de items pas worden opgehaald wanneer ze worden gevraagd.

### List:

- `List` is een concrete klasse in C# die een dynamische array implementeert die items van hetzelfde type opslaat.
- Het biedt functionaliteiten voor het toevoegen, verwijderen, doorzoeken en bewerken van elementen in de lijst.
- In tegenstelling tot `IEnumerable` biedt `List` directe toegang tot elementen op basis van hun index, waardoor willekeurige toegang mogelijk is.
- `List` is ideaal wanneer je een dynamische verzameling nodig hebt met de mogelijkheid om items toe te voegen, te verwijderen of de volgorde van items te wijzigen.

### Gebruiksverschillen:

- Gebruik `IEnumerable` wanneer je alleen iteratiefunctionaliteit nodig hebt en geen behoefte hebt aan directe toegang of bewerking van elementen.
- Gebruik `List` wanneer je een collectie nodig hebt met dynamische grootte en functionaliteit voor toevoegen, verwijderen, en directe toegang tot elementen op basis van hun index.

Kort gezegd, `IEnumerable` is een interface die iteratie mogelijk maakt, terwijl `List` een concrete implementatie is die extra functionaliteit biedt, zoals het beheren van een verzameling van elementen met flexibele grootte en directe toegang tot individuele elementen.