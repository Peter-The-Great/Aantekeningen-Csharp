Ja, je kunt `async void` gebruiken, maar er zijn belangrijke verschillen tussen `async void` en `async Task`.

`async void` wordt meestal gebruikt voor event handlers in GUI-toepassingen (bijvoorbeeld WPF, UWP, WinForms) of bij asynchrone methoden die geen resultaat teruggeven of waarvan het resultaat niet wordt gebruikt of afgewacht. Het belangrijkste kenmerk van `async void` is dat het geen resultaat teruggeeft aan de aanroepende code.

Een voorbeeld van `async void` zou een event handler kunnen zijn:

```cs
private async void Button_Click(object sender, EventArgs e)
{
    await DoSomethingAsync();
    // Geen resultaat om op te wachten, aangezien de methode 'async void' is
}

private async Task DoSomethingAsync()
{
    await Task.Delay(1000);
    Console.WriteLine("Taak voltooid na 1 seconde");
}
```

In dit voorbeeld wordt `async void` gebruikt voor de event handler `Button_Click`. Deze methode roept een andere asynchrone methode `DoSomethingAsync` aan met `await`. Omdat de event handler `async void` is, wordt het resultaat van `DoSomethingAsync` niet opgevangen of afgewacht. Dit kan handig zijn in event handling, maar het kan ook lastig zijn omdat je geen controle hebt over eventuele uitzonderingen die binnen de `async void`-methode worden gegenereerd.

Over het algemeen is het beter om `async Task` te gebruiken, omdat het een taak vertegenwoordigt waarvan je het resultaat kunt opvangen of afwachten, en het biedt ook meer controle over uitzonderingen die in de methode worden gegenereerd. Gebruik `async void` met voorzichtigheid en overweeg het gebruik van `async Task` waar mogelijk, vooral voor methoden waarvan je het resultaat wilt verwerken of waarbij je uitzonderingen correct wilt afhandelen.