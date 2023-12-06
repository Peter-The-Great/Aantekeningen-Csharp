Als je var gebruikt moet je wel het zo doen:
```cs
var s = 'string';
```

Niet zo:
```cs
var s;
```

Want dan weet compiler niet wat je wilt. Dat geld ook binnen in classen.
```cs
class X
{
	public int getal; //Dit is gewoon standaard
	var getal2; //Dit kan niet
	var getal3 = 0; //Dit kan niet
}
var getal4 = 0; //Dit kan
var getal5; //Dit kan
```