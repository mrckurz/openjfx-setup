# JavaFX Setup Guide

Dieser Leitfaden beschreibt, wie man JavaFX auf **Windows**, **macOS** und **Linux** für die Entwicklungsumgebungen **Eclipse**, **VS Code** und **IntelliJ IDEA** einrichtet. Am Ende findest du ein kleines Beispielprogramm.

## Voraussetzungen

- Java Development Kit (JDK) 17 oder neuer (https://adoptium.net)
- JavaFX SDK (https://openjfx.io)

## JavaFX SDK herunterladen

1. Gehe zu https://openjfx.io
2. Lade das passende SDK für dein Betriebssystem herunter
3. Entpacke es an einen gut erreichbaren Ort (z. B. `C:\javafx-sdk` oder `~/javafx-sdk`)

---

## 1. Einrichtung unter Eclipse

### Schritt 1: Eclipse installieren
- https://www.eclipse.org/downloads/
- Wähle "Eclipse IDE for Java Developers"

### Schritt 2: JavaFX in Eclipse konfigurieren

1. Neues Java-Projekt erstellen
2. Rechtsklick auf das Projekt → **Properties** → **Java Build Path**
3. Unter **Libraries** → **Add External JARs...**
   - Wähle alle JAR-Dateien im Ordner `javafx-sdk/lib`
4. Unter **Run Configurations** → **VM arguments**:

   ```
   --module-path /Pfad/zum/javafx-sdk/lib --add-modules javafx.controls,javafx.fxml
   ```

### macOS Hinweis:
Pfad ist z. B. `/Users/deinbenutzername/javafx-sdk/lib`

---

## 2. Einrichtung unter VS Code

### Schritt 1: VS Code installieren
- https://code.visualstudio.com

### Schritt 2: Extensions installieren
- Java Extension Pack
- Debugger for Java
- Maven for Java (optional, wenn Maven verwendet wird)

### Schritt 3: Projektstruktur erstellen

```bash
mkdir javafx-vscode
cd javafx-vscode
mkdir -p src/hellofx .vscode
```

Speichere folgendes als `src/hellofx/HelloFX.java`:

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

### Schritt 4: VS Code konfigurieren

**.vscode/launch.json**
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "java",
      "name": "Launch JavaFX",
      "request": "launch",
      "mainClass": "hellofx.HelloFX",
      "vmArgs": "--module-path /Pfad/zum/javafx-sdk/lib --add-modules javafx.controls,javafx.fxml"
    }
  ]
}
```

**.vscode/settings.json**
```json
{
  "java.project.sourcePaths": ["src"],
  "java.project.referencedLibraries": [
    "/Pfad/zum/javafx-sdk/lib/**/*.jar"
  ]
}
```

### Schritt 5: Projekt öffnen und starten

1. Öffne das Projektverzeichnis in VS Code
2. Öffne die Datei `HelloFX.java`
3. Klicke auf **Run** über der `main`-Methode oder drücke `F5`

**Hinweis:** Der Pfad zur JavaFX-SDK muss zum System und Ort der Entpackung passen.

---

## 3. Einrichtung unter IntelliJ IDEA

### Schritt 1: IntelliJ installieren
- https://www.jetbrains.com/idea/

### Schritt 2: JavaFX-Projekt einrichten

1. Neues Projekt → **JavaFX**
2. In **Project Structure** (Strg+Alt+Shift+S)
   - Unter **Libraries** → **+** → Java
   - Wähle `javafx-sdk/lib`
3. Unter **Run/Debug Configurations** → VM options:

   ```
   --module-path /Pfad/zum/javafx-sdk/lib --add-modules javafx.controls,javafx.fxml
   ```

---

## Beispielprogramm

**Datei:** `src/Main.java`

```java
import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.stage.Stage;

public class Main extends Application {
    public static void main(String[] args) {
        launch(args);
    }

    @Override
    public void start(Stage primaryStage) {
        Label label = new Label("Hello, JavaFX!");
        Scene scene = new Scene(label, 300, 200);
        primaryStage.setScene(scene);
        primaryStage.setTitle("JavaFX Example");
        primaryStage.show();
    }
}
```

---

## Hinweise

- Pfadangaben sind betriebssystemspezifisch:
  - Windows: `C:\\javafx-sdk\\lib`
  - macOS/Linux: `/Users/benutzername/javafx-sdk/lib`
- Benutze Doppelpunkte `:` statt Semikolons `;` auf macOS/Linux in VM options (nur bei Shell-Eingaben relevant)

---

Bei Problemen siehe: https://openjfx.io/openjfx-docs/
