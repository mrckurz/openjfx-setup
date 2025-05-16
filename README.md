# JavaFX Setup Guide

Dieser Leitfaden beschreibt die Einrichtung von JavaFX auf **Windows**, **macOS** und **Linux** für die Entwicklungsumgebungen **Eclipse**, **VS Code** und **IntelliJ IDEA**. Am Ende findest du ein vollständiges Beispielprogramm.

## Voraussetzungen

- Java Development Kit (JDK) 17 oder neuer (https://adoptium.net)
- JavaFX SDK (https://openjfx.io)

## JavaFX SDK herunterladen

1. Gehe zu https://openjfx.io
2. Wähle den passenden Download für dein Betriebssystem
3. Entpacke den Inhalt in ein gut erreichbares Verzeichnis, z. B.:
   - Windows: `C:\javafx-sdk-20.0.1`
   - macOS: `/Users/deinname/javafx-sdk-20.0.1`
   - Linux: `~/javafx-sdk-20.0.1`

---

## 1. Einrichtung unter Eclipse

### Eclipse installieren
- Download: https://www.eclipse.org/downloads/
- Version: „Eclipse IDE for Java Developers“

### Neues Projekt anlegen
1. Datei → Neues Java-Projekt
2. Projektname vergeben

### JavaFX Bibliotheken einbinden
1. Rechtsklick auf Projekt → **Properties**
2. Unter **Java Build Path** → **Libraries** → **Add External JARs**
3. Alle `.jar`-Dateien aus `javafx-sdk/lib` hinzufügen

### VM-Optionen setzen
1. Rechtsklick auf Projekt → **Run As → Run Configurations**
2. Im Tab **Arguments** → **VM arguments** einfügen:

```
--module-path /Pfad/zum/javafx-sdk/lib --add-modules javafx.controls,javafx.fxml
```

---

## 2. Einrichtung unter VS Code

### VS Code installieren
- https://code.visualstudio.com

### Extensions installieren
- Java Extension Pack
- Debugger for Java
- (optional) Maven for Java

### Projektstruktur vorbereiten

```bash
mkdir javafx-vscode
cd javafx-vscode
mkdir -p src/hellofx .vscode
```

### Beispielprogramm speichern unter `src/hellofx/HelloFX.java`

```java
package hellofx;

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.layout.StackPane;
import javafx.stage.Stage;

public class HelloFX extends Application {
    @Override
    public void start(Stage stage) {
        Label label = new Label("Hello, JavaFX!");
        Scene scene = new Scene(new StackPane(label), 400, 200);
        stage.setScene(scene);
        stage.setTitle("HelloFX");
        stage.show();
    }

    public static void main(String[] args) {
        launch();
    }
}
```

### `.vscode/settings.json`

```json
{
  "java.project.sourcePaths": ["src"],
  "java.project.outputPath": "bin",
  "java.project.referencedLibraries": [
    "/Pfad/zur/javafx-sdk/lib/**/*.jar"
  ]
}
```

### `.vscode/launch.json`

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "java",
      "name": "Launch JavaFX",
      "request": "launch",
      "mainClass": "hellofx.HelloFX",
      "vmArgs": "--module-path /Pfad/zur/javafx-sdk/lib --add-modules javafx.controls,javafx.fxml"
    }
  ]
}
```

### Starten

- Öffne die Datei `HelloFX.java` in VS Code
- Klicke auf „Run“ oberhalb der `main`-Methode oder drücke `F5`

---

## 3. Einrichtung unter IntelliJ IDEA

### IntelliJ installieren
- https://www.jetbrains.com/idea/

### Neues Projekt erstellen
1. Neues Projekt → Java
2. Projekt SDK auswählen (z. B. JDK 19)

### JavaFX Bibliothek hinzufügen
1. **File → Project Structure** (`Cmd+,` oder `Strg+Alt+Shift+S`)
2. Reiter **Libraries** → „+“ → **Java**
3. Pfad zu `javafx-sdk/lib` auswählen

### VM Optionen setzen
1. Run → Edit Configurations
2. Im Feld **VM options** einfügen:

```
--module-path /Pfad/zur/javafx-sdk/lib --add-modules javafx.controls,javafx.fxml
```

### Beispielklasse hinzufügen

Datei → Neue Java-Klasse `HelloFX` mit Inhalt:

*(siehe oben unter VS Code Beispiel)*

---

## Hinweise

- **Pfadangaben sind betriebssystemspezifisch:**
  - Windows: `C:\javafx-sdk\lib`
  - macOS/Linux: `/Users/deinname/javafx-sdk/lib`
- Bei **Spaces im Pfad** (z. B. `Application Support`) müssen Anführungszeichen gesetzt werden
- Wenn du ein Modulprojekt nutzt, füge eine `module-info.java` hinzu:

```java
module hellofx {
    requires javafx.controls;
    requires javafx.fxml;
    exports hellofx;
}
```

---

## Weiterführende Links

- [JavaFX Documentation](https://openjfx.io/openjfx-docs/)
- [OpenJFX GitHub Examples](https://github.com/openjfx/samples)
