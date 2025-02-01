
Lab: 'Erstellen eines benutzerdefinierten Agents'
---
<!--
Edit the metadata above to manage the list of exercises in the home page of the GitHub site that gets generated.
You can delete the module and edit index.md in the root of the repo to customize the display so that only the exercises are listed
To enable GitHub page publishing, edit the Page settings for the repo and publish from the main branch
-->

# Erstellen und Testen eines benutzerdefinierten Agents

In dieser Übung erstellen Sie eine Azure OpenAI-Ressource, die als Grundlage für die Erstellung Ihres benutzerdefinierten Agents dient.

Diese Übung dauert ca. **30** Minuten. <!-- update with estimated duration -->

**Hinweis:** Von Lernenden wird erwartet, dass sie diese Übung in ihren eigenen Umgebungen abschließen.

##  Aufgabe 1: Erstellen einer Azure OpenAI-Ressource 

Zunächst müssen Sie ...

1. Navigieren Sie in Ihrem Edge-Browser zu **https://portal.azure.com**.
1. Melden Sie sich beim Azure-Portal an.
2. Wählen Sie oben links auf dem Bildschirm die Option **+ Eine Ressource erstellen** aus.
1. Geben Sie im Suchfeld **Azure OpenAI** ein und drücken Sie die EINGABETASTE.
1. Ein Ergebnis namens **Azure OpenAI** sollte als Option angezeigt werden. In der unteren linken Ecke dieser Option befindet sich eine Schaltfläche mit der Bezeichnung **Erstellen**. Drücken Sie> **Erstellen** > **Azure OpenAI**.
1. Auf der Seite **Azure OpenAI erstellen** legen Sie die folgenden Felder fest: **Hinweis:** Da dieses Lab in der eigenen Umgebung des Lernenden abgeschlossen werden soll, müssen die Lernenden beim Auswählen von Werten für die Felder **Abonnement**, **Tarif** und **Ressourcengruppe** nach eigenem Ermessen vorgehen.
   
   a. **Abonnement** Verwenden Sie beim Ausfüllen dieses Felds Ihr eigenes Ermessen.
   
   b. **Ressourcengruppe** : Verwenden Sie beim Ausfüllen dieses Felds Ihr eigenes Ermessen.
   
   c. **Name** : Geben Sie einen beliebigen Namen ein, den Sie auswählen.
   
   d. **Tarif**: Der Standardwert ist **Standard S0**, aber verwenden Sie beim Ausfüllen dieses Felds Ihr eigenes Ermessen.
   
Wählen Sie **Weiter** aus.

7. Wählen Sie auf der nächsten Seite auf der Registerkarte **Netzwerk** die Option **Alle Netzwerke, einschließlich des Internets, können auf diese Ressource zugreifen** aus.
Wählen Sie **Weiter** aus.
8. Lassen Sie auf der nächsten Seite auf der Registerkarte **Tags** die Felder „Name“ und „Wert“ leer.
Wählen Sie **Weiter** aus.
9. Drücken Sie auf der nächsten Seite auf der Registerkarte **Überprüfen+ Absenden** auf die Option **Erstellen**.
10. Sie gelangen zu einer Seite, auf der diese neu erstellte Azure OpenAI-Ressource erstellt wird. Sie sehen die Meldung **Bereitstellung in Bearbeitung**. Warten Sie einige Sekunden, bis die Bereitstellung dieser Ressource abgeschlossen ist. Klicken Sie nach der Erstellung der Ressource auf die Schaltfläche **Zu Ressource wechseln**.
11. **Ergebnis:** Sie befinden sich jetzt auf der Seite mit neu erstellter Azure OpenAI-Ressource. Sie können dies überprüfen, indem Sie den Namen der Ressource in der oberen linken Ecke der Seite überprüfen. Dieser Name sollte mit dem Namen übereinstimmen, den Sie für Schritt 5c oben ausgewählt haben.


## Aufgabe 2: Implementieren von RAG für das Azure OpenAI-Modell

In dieser Aufgabe erfahren Sie, wie Sie RAG mithilfe einer Datenquelle für Ihre eigene Testumgebung implementieren.

1. Klicken Sie auf der Seite für Ihre neu erstellte Azure OpenAI-Ressource im Menüband oben auf der Seite auf **Zum Azure AI Foundry-Portal wechseln**.
2. Wählen Sie auf der neuen Seite **Chat-Playground** unter **Setup** die Option **+ Neue Bereitstellung erstellen** > **Aus Basismodellen** aus.
3. Scrollen Sie im Popupfenster mit dem Titel **Chatabschlussmodell auswählen** nach unten, und wählen Sie die Option **gpt-4o** > **Bestätigen** aus.
4. Lassen Sie im Fenster **Modell gtp-4o bereitstellen** alles in der Standardeinstellung, und wählen Sie **Bereitstellen** aus.
5. Wählen Sie auf der Seite **Chat-Playground** die Option **Daten hinzufügen** am unteren Rand des Bildschirms aus, > **+ Eine Datenquelle hinzufügen**.
6. Wählen Sie im Fenster **Datenquelle auswählen oder hinzufügen** die Option **Datenquelle auswählen** aus der Dropdownliste aus und wählen Sie die Option **Dateien hochladen (Vorschau)** aus.
7. Stellen Sie auf der nächsten Seite für die Option **Datenquelle** sicher, dass die Dropdownliste für **Datenquelle auswählen** auf **Dateien hochladen (Vorschau)** festgelegt ist.
   
   a. Stellen Sie im Feld **Abonnement** sicher, dass der Standardwert ausgewählt ist.
   
    b. Wählen Sie im Feld **Azure Blob Storage-Ressource auswählen** die Option **Neue Azure Blob Storage-Ressource erstellen** aus > Stellen Sie im neuen Fenster mit dem Titel **Speicherkonto erstellen** auf der Registerkarte **Grundlagen** sicher, dass die Felder **Abonnement** und **Ressourcengruppe** auf die Standardwerte festgelegt sind und wählen Sie den einzigen verfügbaren Wert für **Ressourcengruppe** aus. Geben Sie unter **Instanzdetails** einen Namen für den **Namen des Speicherkontos** an. Lassen Sie die restlichen Felder unverändert. Klicken Sie auf **Überprüfen + erstellen**. Wählen Sie auf der Registerkarte **Überprüfen + Erstellen** die Schaltfläche **Erstellen** aus. Die Bereitstellung der Azure Blob Storage-Ressource dauert einen Moment.
   
   c. Navigieren Sie zurück zum Fenster für den **Chat-Playground**. Wählen Sie die Schaltfläche „Aktualisieren“ neben dem Feld **Azure Blob Storage-Ressource auswählen** aus, > wählen Sie die Ressource aus, die Sie in Schritt b oben erstellt haben. Wählen Sie die Schaltfläche **CORS aktivieren** aus.
   
8. Wählen Sie für das Feld **Azure KI Search-Ressource** auswählen die Option **Neue Azure AI Search-Ressource erstellen** aus.  Stellen Sie sicher, dass die Felder **Abonnement** und **Ressourcengruppe** auf Werte Ihrer Wahl festgelegt sind. **Hinweis:** Da diese Übung in der eigenen Umgebung des Lernenden abgeschlossen werden soll, müssen die Lernenden beim Auswählen von Werten für die Felder **Abonnement** und **Ressourcengruppe** nach eigenem Ermessen vorgehen. Klicken Sie auf den Dropdownwert für **Ressourcengruppe**, um die gewünschte Option auszuwählen. Geben Sie einen **Dienstnamen** ein, > Stellen Sie sicher, dass alle anderen Felder auf die Standardwerte festgelegt sind, > wählen Sie **Überprüfen + Erstellen** > **Erstellen** aus. Die Bereitstellung der Azure KI Search-Ressource dauert einen Moment.
9. Navigieren Sie zurück zum Fenster für den **Chat-Playground**. Wählen Sie die Schaltfläche „Aktualisieren“ neben dem Feld **Azure Blob Storage-Ressource auswählen** aus, > wählen Sie die Ressource aus, die Sie in Schritt 9 oben erstellt haben.
10. Geben Sie einen Namen für das Feld **Indexname eingeben** > **Weiter** aus. Kopieren Sie diesen Namen, und fügen Sie ihn an einer zugänglichen Stelle ein, da Sie ihn für die anstehenden Aufgaben benötigen werden.
11. Wählen Sie im Abschnitt **Dateien hochladen** die Option **Nach einer Datei suchen** aus > Navigieren Sie im Datei-Explorer zu **Dokumente** > wählen Sie alle drei Dateien aus: **ContosoAI ChipEnhance Perks Program.docx**, **ContosoAI Insurance Plans.docx** und **Overview of ContosoAI.docx** > **Öffnen** > Die drei Dateien sollten nun auf der Seite **Dateien hochladen** des Fensters angezeigt werden > Wählen Sie **Dateien hochladen** > **Weiter** aus.
12. Lassen Sie im Abschnitt **Datenverwaltung** alles als Standard, und wählen Sie **Weiter** aus.
13. Wählen Sie unter **Datenverbindung** die Option **API-Schlüssel** > **Weiter** > **Speichern und schließen** aus.
14. Wählen Sie im Fenster **Chat-Playground** die Option **Code anzeigen** aus, der sich im Menüband oben links im Fenster befindet.
15. Wählen Sie im Fenster **Beispielcode** die Dropdownliste rechts neben dem ersten Feld aus, und wählen Sie **json** aus > wechseln Sie zur Registerkarte **Schlüsselauthentifizierung**:
    
    a. Kopieren Sie die folgenden Werte, und fügen Sie sie ein, da Sie sie in den anstehenden Aufgaben benötigen: **Endpunkt**, **API-Schlüssel** und **Azure Search-Ressourcenschlüssel**.  Sie können dieses Fenster auch geöffnet lassen, um diese Werte für die anstehenden Aufgaben zu sammeln.

 ## Aufgabe 3: Erstellen und Testen eines benutzerdefinierten Agents in Testtool und Teams

In dieser Aufgabe erstellen Sie den benutzerdefinierten Agent und testen den Agent.

1. Öffnen Sie **Visual Studio Code**.
2. Wählen Sie auf der rechten Seite des Visual Studio-Codefensters das Symbol **Teams Toolkit** aus > wählen Sie die Option **Neue App erstellen** aus > wählen Sie in der Dropdownliste **Benutzerdefinierter Modul-Agent** aus (Hinweis: Je nach Version des Teams-Toolkits müssen Sie möglicherweise die Option **Benutzerdefinierter Copilot** auswählen) > **Basic-KI-Chatbot** > **JavaScript** > **Azure OpenAI.**.
3. Geben Sie im leeren Feld oben auf dem Bildschirm zuerst Folgendes ein:

   a. **API-Schlüssel** aus der vorherigen Aufgabe > **Eingeben**.

   b. **Endpunkt** aus der vorherigen Aufgabe > **Eingeben**.

   c. Geben Sie für **Azure Open AI-Bereitstellungsname** die Option **gpt-4o** > **Eingeben** ein.

   d. Wählen Sie für **Ordner auswählen, in dem sich Ihr Projektraumordner befindet** die Option **Standardordner** aus.

   e. Für **Eingabe des Anwendungsnamens** geben Sie einen beliebigen Namen ein > **Eingabe**> im Pop-up-Fenster wählen Sie **Ja, ich vertraue den Autoren** aus.

   f. Navigieren Sie im neuen VS Code-Fenster der neu erstellten App aus den Schritten a-f oben zum Symbol **Teams-Toolkit** auf der linken Seite des Bildschirms.

   **Hinweis:** Die Schritte g–i sollten für die Umgebung eines Benutzers abgeschlossen werden, der keinen Administratorzugriff auf das Microsoft Teams Admin Center hat. Wenn Benutzer stattdessen über einen M365-Mandanten mit Administratorzugriff verfügen, führen Sie stattdessen die Schritte j–m aus.

   g. Klicken Sie im Abschnitt **Konten** auf **Bei Microsoft 365 anmelden**. Es öffnet sich ein neues Fenster in Ihrem Browser. Melden Sie sich mit den bereitgestellten Anmeldeinformationen an.

   h. Navigieren Sie zurück zur VS-Codeseite Ihrer App. Nun sollte ein grünes Häkchen mit den Wörtern **Benutzerdefinierter App-Upload aktiviert** unter **Konten angezeigt werden.

   i. Klicken Sie im Abschnitt **Konten** auf **Bei Azure anmelden**. Klicken Sie in jedem Popupfenster auf **OK**. Es öffnet sich ein neues Fenster in Ihrem Browser. Melden Sie sich mit den bereitgestellten Anmeldeinformationen an.

   Für Benutzer, die über einen M365-Mandanten mit Administratorzugriff auf das Microsoft Teams Admin Center verfügen, führen Sie bitte die folgenden Schritte anstelle der oben aufgeführten Schritte aus:

   j. Melden Sie sichhttps://admin.teams.microsoft.commit Ihren Administratoranmeldeinformationen an.

   k. Wechseln Sie auf der Randleiste zu **Teams-Apps** , und wählen Sie dann  **Setuprichtlinien** aus.

   l. Wählen Sie die  **Globale Richtlinie (organisationsweite Standardeinstellung)**  aus, und aktivieren Sie dann die Umschaltfläche  **Benutzerdefinierte Apps hochladen** .

   m. Scrollen Sie nach unten, und wählen Sie die Schaltfläche  **Speichern**  aus, um die Firewalländerungen zu speichern. Ihr Mandant ist jetzt so konfiguriert, dass das Querladen von benutzerdefinierten Apps zulässig ist. 
   
5. Navigieren Sie im VS-Codefenster Ihrer App zu **src/prompts/chat/skprompt.txt**. Löschen Sie jeglichen Text in der Datei, und fügen Sie Folgendes ein: „Es folgt eine Unterhaltung mit einem KI-Assistenten, der Experte für die Beantwortung von Fragen in dem gegebenen Kontext ist. 

Antworten sollten in einem kurzen journalistischen Stil mit nicht mehr als 80 Wörtern erfolgen.“ 

5. Navigieren Sie im VS-Codefenster Ihrer App unter „Eingabeaufforderungen/Chat“ zur Datei **config.json**. Löschen Sie den Code, der derzeit in den Klammern vorhanden ist, und fügen Sie den folgenden Code in die Klammern ein.

```json
"data_sources": [ 
    { 
        "type": "azure_search", 
        "parameters": { 
            "endpoint": "AZURE-AI-SEARCH-ENDPOINT", 
            "index_name": "YOUR-INDEX_NAME",
            "in_scope": false,
            "authentication": { 
                "type": "api_key", 
                "key": "AZURE-AI-SEARCH-KEY" 
            } 
        } 
    } 
]
```

6. Ersetzen Sie im obigen Code Folgendes durch die Werte, die Sie aus der vorherigen Aufgabe gespeichert haben (Hinweis: Die Werte müssen in Anführungszeichen stehen):

   a. **AZURE-AI-SEARCH-ENDPOINT** ist der **Endpunkt** aus der vorherigen Aufgabe.

   b. **index_name** ist der **Indexname** aus Aufabe 2 Schritt 11 in der vorherigen Aufgabe.

   c. **Schlüssel** ist der **Azure Search-Ressourcenschlüssel** aus der vorherigen Aufgabe.

7. Wechseln Sie zur Datei **src/app/app.js** und fügen Sie die folgende Variable in  **OpenAIModel** direkt hinter der Zeile azureEndpoint hinzu: config.azureOpenAIEndpoint, : 

    a. azureApiVersion: '2024-02-15-preview',
   
8. **Datei** > **Alle speichern**
    
9. Drücken Sie **STRG+UMSCHALT+d** auf Ihrer Tastatur. Oben links wird eine Dropdownliste mit einer grünen Wiedergabetaste und dem Wort „Debuggen“ angezeigt > Wählen Sie die Dropdownlist aus > Wählen Sie **Debuggen im Test-Tool** aus > Drücken Sie **F5**.
10. Der benutzerdefinierte Engine Agent wird innerhalb des von Ihnen ausgewählten Debuggingtools ausgeführt, das in Ihrem Browser geöffnet wird. Sie können dem Bot alle Fragen zu den RAG-Daten stellen, die in Aufgabe 2 Schritt 12 hochgeladen wurden.
11. Navigieren Sie zurück zum VS-Codefenster für Ihre App. Wählen Sie das Dropdown-Menü **Debuggen** aus und wählen Sie die Option **Debuggen in Teams (Edge)** aus. Drücken Sie dann **F5** oder die grüne Wiedergabetaste.
13. Es öffnet sich ein neues Fenster in Ihrem Edge-Browser. Sie werden aufgefordert, sich anzumelden. Verwenden Sie die zum Anmelden bereitgestellten Anmeldeinformationen. Wenn Sie sich erfolgreich angemeldet haben, können Sie das Fenster schließen.
14. Wiederholen Sie Schritt 11 noch einmal. Es sollte ein Fenster mit dem Titel Ihrer neu erstellten App angezeigt werden. Wählen Sie **Hinzufügen** > **Öffnen** aus.
15. Herzlichen Glückwunsch! Sie können dem Agent jetzt jede Frage zu den RAG-Datendateien stellen.
16. **Hinweis:** Da dieser Agent mit Ihrem eigenen Abonnement für Bildungszwecke erstellt wurde, sollten die Benutzenden den Agent nach Abschluss dieses Labs löschen. Um einen benutzerdefinierten Agent in Microsoft Teams zu löschen, können Sie wie folgt vorgehen:
- Wählen Sie den zu löschenden Agent, dann das Symbol **Weitere Optionen (...)** und schließlich **Löschen** aus.
- Entfernen Sie den Agent aus einem Chat, indem Sie die Auslassungspunkte im Thread und dann **Apps verwalten** auswählen.
- Wählen Sie in der Benutzeroberfläche für die Erstellung eines Agents die **Auslassungspunkte (...)** und dann **Löschen** aus.

**ENDE DES LABS**
