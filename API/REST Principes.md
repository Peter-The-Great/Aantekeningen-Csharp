REST (Representational State Transfer) is een architectuurstijl die wordt gebruikt bij het ontwerpen van web-API’s. REST is gebaseerd op zes architecturale beperkingen die zorgen voor eenvoud, schaalbaarheid en statelessness in het ontwerp. De zes beperkingen zijn:

1. Uniforme interface: door de principes van algemeenheid toe te passen op de componenteninterface, kan de algehele systeemarchitectuur worden vereenvoudigd en de zichtbaarheid van interacties worden verbeterd. REST definieert een consistente en uniforme interface voor interacties tussen clients en servers. De interface moet de resources uniek identificeren, de manipulatie van resources via representaties mogelijk maken, zelfbeschrijvende berichten bevatten en hypermedia als de motor van de applicatiestatus gebruiken.
    
2. Client-server: de client-serverarchitectuur scheidt de verantwoordelijkheden van de gebruikersinterface van de gegevensopslag en -verwerking. Dit maakt het mogelijk dat de componenten onafhankelijk van elkaar kunnen evolueren.
    
3. Stateless: elke aanvraag van de client naar de server moet alle informatie bevatten die nodig is om de aanvraag te begrijpen. De server mag geen context opslaan tussen aanvragen.
    
4. Cacheable: clients kunnen reacties opslaan om toekomstige aanvragen te vermijden.
    
5. Layered system: een client kan niet zien of hij rechtstreeks met de server communiceert of via een tussenliggende tussenlaag.
    
6. Code on demand (optioneel): servers kunnen optioneel uitvoerbare code naar de client sturen om de functionaliteit van de client uit te breiden.

Bronnen:
[1. restfulapi.net](https://restfulapi.net/)[2. amplication.com](https://amplication.com/blog/rest-apis-what-why-and-how)[3. restfulapi.net](https://restfulapi.net/rest-architectural-constraints/)[4. ibm.com](https://www.ibm.com/topics/rest-apis)