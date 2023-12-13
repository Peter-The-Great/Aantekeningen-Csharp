Bronnen: [1. Microsoft Learn](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/websockets?view=aspnetcore-8.0)
Hier is een voorbeeld van hoe je een WebSocket-server kunt maken in C#:

```csharp
using System;
using System.Net;
using System.Net.Sockets;
using System.Text;
using System.Threading.Tasks;

class Program
{
    static async Task Main(string[] args)
    {
        TcpListener server = new TcpListener(IPAddress.Parse("127.0.0.1"), 8080);
        server.Start();
        Console.WriteLine("Server gestart op 127.0.0.1:8080. Wacht op verbinding...");

        TcpClient client = await server.AcceptTcpClientAsync();
        Console.WriteLine("Een client verbonden.");

        NetworkStream stream = client.GetStream();

        byte[] buffer = new byte[1024];
        int bytesRead = await stream.ReadAsync(buffer, 0, buffer.Length);
        string request = Encoding.UTF8.GetString(buffer, 0, bytesRead);

        Console.WriteLine("Ontvangen bericht: " + request);

        string response = "Hallo, wereld!";
        byte[] data = Encoding.UTF8.GetBytes(response);

        await stream.WriteAsync(data, 0, data.Length);
        Console.WriteLine("Verzonden bericht: " + response);

        client.Close();
        server.Stop();
    }
}
```

In dit voorbeeld wordt een WebSocket-server gemaakt die luistert op poort 8080. Wanneer een client verbinding maakt met de server, wordt er een bericht ontvangen en wordt er een antwoord verzonden.


## Hoe gebruik ik ze in ASP.NET
WebSockets is een protocol dat full-duplex communicatie biedt over een enkele TCP-verbinding. Het wordt vaak gebruikt in webapplicaties die real-time communicatie vereisen, zoals chat-apps, dashboard-apps en game-apps. In ASP.NET Core kun je WebSockets gebruiken om real-time communicatie te implementeren tussen een webbrowser en een webserver.

Om WebSockets te gebruiken in ASP.NET Core, moet je de `Microsoft.AspNetCore.WebSockets`-package installeren via NuGet. Vervolgens moet je de WebSockets-middleware toevoegen aan de app-pijplijn in de `Configure`-methode van de `Startup`-klasse:

```csharp
app.UseWebSockets();
```

Vervolgens moet je een WebSocket-endpoint definiëren in de `Map`-methode van de `UseEndpoints`-methode van de `Startup`-klasse:

```csharp
app.UseEndpoints(endpoints =>
{
    endpoints.MapWebSocket("/ws", () => new MyWebSocketHandler());
});
```

In dit voorbeeld wordt een WebSocket-endpoint gedefinieerd op het pad “/ws”. Wanneer een client verbinding maakt met dit endpoint, wordt er een nieuwe instantie van de `MyWebSocketHandler`-klasse gemaakt om de communicatie af te handelen.

Hier is een voorbeeld van hoe je een WebSocket-handler kunt maken in ASP.NET Core:

```csharp
public class MyWebSocketHandler : WebSocketHandler
{
    public MyWebSocketHandler(WebSocketConnectionManager webSocketConnectionManager) : base(webSocketConnectionManager)
    {
    }

    public override async Task ReceiveAsync(WebSocket socket, WebSocketReceiveResult result, byte[] buffer)
    {
        string message = Encoding.UTF8.GetString(buffer, 0, result.Count);
        await SendMessageToAllAsync(message);
    }
}
```

In dit voorbeeld wordt de `MyWebSocketHandler`-klasse gedefinieerd als een WebSocket-handler. De `ReceiveAsync`-methode wordt overschreven om de ontvangen berichten te verwerken. In dit geval wordt het ontvangen bericht doorgestuurd naar alle aangesloten clients.

Het is belangrijk om de beveiliging van WebSockets in acht te nemen bij het implementeren van real-time communicatie in een webapplicatie. Hier zijn enkele tips om de beveiliging van WebSockets in ASP.NET Core te verbeteren:

1. Gebruik HTTPS om de communicatie tussen de webbrowser en de webserver te versleutelen.
2. Implementeer authenticatie en autorisatie om ervoor te zorgen dat alleen geautoriseerde gebruikers toegang hebben tot de real-time communicatie.
3. Gebruik SSL/TLS-certificaten om de identiteit van de webserver te verifiëren en de integriteit van de communicatie te waarborgen.
4. Implementeer rate limiting om te voorkomen dat kwaadwillende gebruikers de server overbelasten met te veel verzoeken.
5. Gebruik inputvalidatie om te voorkomen dat kwaadwillende gebruikers schadelijke gegevens naar de server sturen.

## Verschil tussen HTTP en WebSocket
HTTP (Hypertext Transfer Protocol) en WebSocket zijn beide communicatieprotocollen die worden gebruikt in client-servercommunicatie. HTTP is een unidirectioneel protocol waarbij de client een verzoek stuurt en de server een antwoord stuurt. Het wordt vaak gebruikt om gegevens op te halen van een server, zoals HTML-documenten, afbeeldingen, toepassingsgegevens (JSON) en meer. Aan de andere kant is WebSocket een bidirectioneel protocol dat is ontworpen om realtime communicatie tussen de server en de client mogelijk te maken. Het maakt het mogelijk om continu gegevens te verzenden en ontvangen zonder dat er een nieuw verzoek nodig is. Dit is handig voor toepassingen die real-time gegevens nodig hebben, zoals chat-apps, dashboard-apps en game-apps.

HTTP-communicatie volgt het request-response-messagingpatroon waarbij de client een verzoek doet en de webserver een antwoord stuurt dat niet alleen de gevraagde inhoud bevat, maar ook relevante informatie over het verzoek. Onder de motorkap wordt voor elk verzoek een kortstondige verbinding met de server geopend en vervolgens gesloten. Aan de andere kant maakt WebSocket-communicatie gebruik van een enkele TCP-verbinding die continu open blijft. Dit maakt het mogelijk om gegevens te verzenden en ontvangen zonder dat er een nieuw verzoek nodig is.