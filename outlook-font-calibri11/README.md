# Standard-Schriftarten und -Stile für Outlook über Intune setzen

## Einführung
Diese Anleitung beschreibt, wie Sie die Standard-Schriftarten und -Stile für Microsoft Outlook über Microsoft Intune festlegen können. Dies wird durch die Bereitstellung eines PowerShell-Skripts realisiert, das die aktuellen Outlook-Schriftarteneinstellungen überprüft und ggf. korrigiert.

## Voraussetzungen
- Microsoft Intune-Abonnement
- Windows 10/11 mit Microsoft Outlook installiert
- Berechtigungen zur Bereitstellung von PowerShell-Skripten über Intune

## Enthaltene Skripte
- `DetectOutlookFont.ps1`: Erkennt die aktuellen Schriftarteneinstellungen von Outlook.
- `RemediateOutlookFont.ps1`: Setzt die gewünschten Schriftarten und Stile, falls sie nicht den Vorgaben entsprechen.

## Einrichtung in Microsoft Intune

### 1. Anmeldung bei Microsoft Endpoint Manager
1. Melden Sie sich im [Microsoft Endpoint Manager Admin Center](https://endpoint.microsoft.com/) an.
2. Navigieren Sie zu **Geräte** → **Windows** → **PowerShell-Skripte**.

### 2. Erstellen eines neuen Skript-Deployments
1. Klicken Sie auf **Hinzufügen**.
2. Geben Sie einen Namen für das Skript ein, z. B. `Outlook Standard-Schriftart setzen`.
3. Wählen Sie **Hochladen** und laden Sie die Datei `DetectOutlookFont.ps1` hoch.
4. Setzen Sie die folgenden Konfigurationen:
   - **Skript ausführen als**: `System`
   - **Skriptausführung bei Benutzern mit eingeschränkten Rechten zulassen**: `Ja`
   - **Protokollierung von Skript-Ausgaben aktivieren**: `Ja`
5. Klicken Sie auf **Weiter** und weisen Sie das Skript der gewünschten Gruppe von Geräten oder Benutzern zu.

### 3. Erstellen der Korrekturrichtlinie (Remediation Script)
1. Wiederholen Sie die obigen Schritte für das Skript `RemediateOutlookFont.ps1`.
2. Stellen Sie sicher, dass das Skript als **Remediation Script** konfiguriert wird.
3. Aktivieren Sie in Intune die **Fehlerbehebung (Remediation)**-Option für das Skript.
4. Weisen Sie das Skript ebenfalls den relevanten Geräten oder Benutzern zu.

## Funktionsweise
- `DetectOutlookFont.ps1` überprüft, ob die gewünschten Schriftarten und Stile in Outlook richtig gesetzt sind.
- Falls Abweichungen erkannt werden, setzt `RemediateOutlookFont.ps1` die korrekten Werte.
- Das Skript wird regelmäßig über Intune ausgeführt, um sicherzustellen, dass die Einstellungen nicht manuell geändert werden.

## Überprüfung der Umsetzung
1. Melden Sie sich bei einem verwalteten Gerät an.
2. Öffnen Sie die Windows PowerShell und führen Sie den Befehl aus:
   ```powershell
   Get-IntuneManagementExtensionLog
   ```
3. Überprüfen Sie das Log auf Fehler oder erfolgreiche Änderungen.

## Fehlerbehebung
Falls das Skript nicht wie erwartet funktioniert:
- Stellen Sie sicher, dass das Gerät korrekt mit Intune registriert ist.
- Prüfen Sie die Protokolle in `C:\ProgramData\Microsoft\IntuneManagementExtension\Logs`.
- Testen Sie das Skript manuell auf einem Gerät, bevor es über Intune ausgerollt wird.

## Fazit
Mit dieser Methode können Unternehmen die Schriftarteneinstellungen von Outlook standardisieren und sicherstellen, dass sie unternehmensweit konsistent bleiben. Das Skript bietet eine einfache und effektive Möglichkeit, dies über Microsoft Intune zu verwalten, insbesondere durch die Nutzung der **Remediation Script**-Funktion zur kontinuierlichen Überwachung und Korrektur der Einstellungen.
