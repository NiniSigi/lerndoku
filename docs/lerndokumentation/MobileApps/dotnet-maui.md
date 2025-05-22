---
title: ".NET MAUI"
sidebar_position: 2
---

# .NET MAUI

Im Rahmen eines Kundenprojekts für [ZAK](https://www.cler.ch/de/info/zak) habe ich die Möglichkeit gehabt mich intensiv mit .NET MAUI auseinander zu setzen. Das war für mich eine sehr spannende Erfahrung da ich vorher hauptsächlich mit Web-Technologien gearbeitet habe und jetzt in die Welt der nativen App-Entwicklung eingetaucht bin.

## Was ist .NET MAUI und wie habe ich es gelernt?

.NET MAUI (Multi-platform App UI) ist das neueste Cross-Platform-Framework von Microsoft für die Entwicklung von nativen Apps. Es ist der Nachfolger von Xamarin.Forms und wurde 2022 veröffentlicht. Mit .NET MAUI kann man Apps für iOS, Android, Windows und macOS entwickeln.

### Meine Lernreise mit .NET MAUI

**Wie ich .NET MAUI gelernt habe**
Pani hat mir zwei sehr gute Bücher ausgeliehen die mir beim Lernen von .NET MAUI geholfen haben. Ohne diese Bücher wäre es für mich viel schwieriger gewesen mich in das Framework einzuarbeiten. Die Bücher haben mir die Grundlagen und auch fortgeschrittene Konzepte sehr gut erklärt.

**ZAK - Die erste echte Schweizer Bank auf dem Smartphone**
ZAK ist eine innovative Schweizer Bank die komplett digital funktioniert. Sie bietet ein kostenloses Konto, eine gratis Visa Debitkarte und verschiedene Spar- und Vorsorgeprodukte an. Die App wurde speziell für Smartphones entwickelt und bietet Funktionen wie TWINT-Integration, eBill, Mobile Payment und gemeinsame Töpfe für Gruppenausgaben.

**Code-First Ansatz**
Ein wichtiger Unterschied von unserem Projektzu anderen .NET MAUI projekten ist das wir bei ZAK mit Code-First arbeiten. Das bedeutet wir schreiben keine XML/XAML-Dateien sondern definieren die UI direkt im C#-Code. Das macht die Entwicklung viel flexibler und einfacher zu debuggen.

## Was macht .NET MAUI so besonders?

### 1. **C# als Programmiersprache**
.NET MAUI nutzt C# als Programmiersprache, was für mich als .NET-Entwickler sehr vertraut war. C# ist eine moderne, objektorientierte Sprache mit vielen mächtigen Features wie LINQ, async/await und generische Typen. Das war für mich ein grosser Vorteil weil ich C# schon kannte.

### 2. **Native Performance**
.NET MAUI kompiliert zu nativen Code für jede Plattform. Das bedeutet die Apps haben die gleiche Performance wie nativ entwickelte Apps. Das ist echt cool weil man nicht auf Performance verzichten muss.

### 3. **MVVM Pattern**
.NET MAUI ist speziell für das MVVM (Model-View-ViewModel) Pattern optimiert. Das macht die Architektur sauber und wartbar. Das war für mich neu aber die Bücher von Pani haben mir das sehr gut erklärt.

## MVVM Pattern erklärt

### Was ist MVVM?
MVVM (Model-View-ViewModel) ist ein Architekturpattern das die UI-Logik von der Geschäftslogik trennt. Es besteht aus drei Hauptkomponenten:

#### **Model**
Das Model repräsentiert die Daten und Geschäftslogik. Es enthält keine UI-spezifischen Informationen.

```csharp
public class Customer
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
    public DateTime CreatedDate { get; set; }
}
```

#### **View**
Die View ist die UI-Schicht. Sie zeigt die Daten an und leitet Benutzerinteraktionen an das ViewModel weiter.

```csharp
public partial class CustomerPage : ContentPage
{
    public CustomerPage()
    {
        InitializeComponent();
        BindingContext = new CustomerViewModel();
    }
}
```

#### **ViewModel**
Das ViewModel ist die Verbindung zwischen Model und View. Es enthält die Präsentationslogik und verwaltet den Zustand der View.

```csharp
public class CustomerViewModel : ObservableObject
{
    private Customer _customer;
    
    public Customer Customer
    {
        get => _customer;
        set => SetProperty(ref _customer, value);
    }
    
    public ICommand SaveCommand { get; }
    
    public CustomerViewModel()
    {
        SaveCommand = new Command(ExecuteSave);
    }
    
    private void ExecuteSave()
    {
        // Geschäftslogik hier
    }
}
```

### Vorteile von MVVM
- **Trennung der Zuständigkeiten**: Jede Komponente hat eine klare Aufgabe
- **Testbarkeit**: ViewModels können einfach unit-getestet werden
- **Wiederverwendbarkeit**: ViewModels können in verschiedenen Views verwendet werden
- **Maintainability**: Code ist sauber strukturiert und leicht zu warten

Das MVVM Pattern war für mich erstmal verwirrend aber durch die Bücher von Pani habe ich es schnell verstanden. Es macht den Code viel sauberer und einfacher zu warten.
Jedoch gibt es auch heute noch momente bei denen ich es Überhaubt nicht versthehe. 

## .NET MAUI Grundlagen

### Projektstruktur
So sieht eine typische .NET MAUI Projektstruktur ohne Code First ansatz aus:
```
MyApp/
├── Platforms/
│   ├── Android/
│   ├── iOS/
│   ├── MacCatalyst/
│   └── Windows/
├── Resources/
│   ├── Images/
│   └── Fonts/
├── App.xaml
├── App.xaml.cs
├── MainPage.xaml
└── MainPage.xaml.cs
```

### Code-First UI Beispiel
```csharp
public partial class MainPage : ContentPage
{
    public MainPage()
    {
        InitializeComponent();
        
        Content = new StackLayout
        {
            Children =
            {
                new Label
                {
                    Text = "Willkommen bei .NET MAUI!",
                    HorizontalOptions = LayoutOptions.Center,
                    VerticalOptions = LayoutOptions.Center
                },
                new Button
                {
                    Text = "Klick mich",
                    Command = new Command(() => DisplayAlert("Hallo", "Button geklickt!", "OK"))
                }
            }
        };
    }
}
```

### Data Binding
```csharp
// ViewModel
public class MainViewModel : ObservableObject
{
    private string _title;
    
    public string Title
    {
        get => _title;
        set => SetProperty(ref _title, value);
    }
}

// View
<Label Text="{Binding Title}" />
```

### Navigation
```csharp
// Navigation zu einer neuen Seite
await Navigation.PushAsync(new DetailPage());

// Zurück zur vorherigen Seite
await Navigation.PopAsync();
```

### Dependency Injection
```csharp
// In MauiProgram.cs
builder.Services.AddSingleton<ICustomerService, CustomerService>();
builder.Services.AddTransient<CustomerViewModel>();

// In ViewModel
public CustomerViewModel(ICustomerService customerService)
{
    _customerService = customerService;
}
```

## Nützliche Ressourcen

### Offizielle Dokumentation
Das sind die wichtigsten Links die ich benutzt habe:
- [.NET MAUI Documentation](https://docs.microsoft.com/en-us/dotnet/maui/)
- [C# Language Reference](https://docs.microsoft.com/en-us/dotnet/csharp/)
- [MVVM Pattern Guide](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/enterprise-application-patterns/mvvm)

### Community-Ressourcen
Die Community ist echt hilfreich:
- [.NET MAUI Community Toolkit](https://github.com/CommunityToolkit/Maui)
- [NuGet.org](https://www.nuget.org/) - Hier findest du alle Pakete
- [.NET MAUI Samples](https://github.com/dotnet/maui-samples)

### Lernressourcen
Das hat mir beim Lernen geholfen:
- [.NET MAUI Tutorials](https://docs.microsoft.com/en-us/dotnet/maui/tutorials/)
- [.NET MAUI YouTube Channel](https://www.youtube.com/c/dotnet)
- [.NET MAUI Workshop](https://github.com/dotnet-presentations/dotnet-maui-workshop)

**Bücher von Pani**
Die zwei Bücher die mir Pani ausgeliehen hat waren echt Gold wert. Ohne diese wäre es für mich viel schwieriger gewesen .NET MAUI zu lernen. Die Bücher haben mir die Grundlagen und auch fortgeschrittene Konzepte sehr gut erklärt. Pani hat die über Netcetra gekauft und ich denke das er sie euch auch ausleihen würde bei intresse.

## Fazit

.NET MAUI hat sich als echt gute Wahl für das ZAK-Banking-Projekt rausgestellt. Die Kombination aus Code-First-Entwicklung, MVVM-Pattern und nativer Performance macht .NET MAUI zu einem echt mächtigen Werkzeug für moderne Cross-Platform-App-Entwicklung. Die Bücher von Pani haben mir dabei sehr geholfen.