---
title: So funktioniert die Benutzerkontosteuerung
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: da83ddb2-6182-417c-aa8e-0b47b2e17d13
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/12/2016
ms.openlocfilehash: 66af2af28a1c26920e906f58f738e25d5032c4c1
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89639448"
---
# <a name="how-user-account-control-works"></a>So funktioniert die Benutzerkontosteuerung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mithilfe der Benutzerkontensteuerung (User Account Control, UAC) können Computer gegen Schäden durch Schadsoftware (auch als "Malware" bezeichnet) geschützt werden, sodass Organisationen besser verwaltete Desktops bereitstellen können. Dank UAC werden Anwendungen und Aufgaben immer im Sicherheitskontext eines Kontos ohne Administratorberechtigungen ausgeführt, es sei denn, ein Administrator autorisiert gezielt Administratorzugriff zum System. UAC kann die automatische Installation nicht autorisierter Anwendungen blockieren und unbeabsichtigte Änderungen an den Systemeinstellungen verhindern.

## <a name="uac-process-and-interactions"></a>UAC-Prozess und Interaktionen
Jede Anwendung, die das Administrator Zugriffs Token erfordert, muss den Administrator zur Zustimmung auffordern. Die einzige Ausnahme ist die Beziehung, die zwischen den über- und den untergeordneten Prozessen besteht. Untergeordnete Prozesse erben das Benutzer Zugriffs Token vom übergeordneten Prozess. Allerdings müssen sowohl die über- als auch die untergeordneten Prozesse die gleiche Integritätsebene besitzen. Windows Server 2012 schützt Prozesse durch Markieren Ihrer Integritäts Ebenen. Integritätsebenen geben Aufschluss über die Vertrauenswürdigkeit. Eine Anwendung mit „hoher“ Integrität führt Aufgaben aus, die Systemdaten ändern, beispielsweise eine Anwendung für die Datenträgerpartitionierung. Demgegenüber führt eine Anwendung mit „niedriger“ Integrität Aufgaben aus, die das Betriebssystem potenziell gefährden könnten, beispielsweise ein Webbrowser. Anwendungen mit niedrigeren Integritäts Stufen können Daten in Anwendungen mit höheren Integritäts Stufen nicht ändern. Wenn ein Standardbenutzer versucht, eine Anwendung auszuführen, die ein Administrator Zugriffs Token erfordert, erfordert UAC, dass der Benutzer gültige Administrator Anmelde Informationen bereitstellt.

Um besser zu verstehen, wie dieser Prozess passiert, ist es wichtig, die Details zum Anmeldevorgang von Windows Server 2012 zu überprüfen.

### <a name="windows-server-2012-logon-process"></a>Windows Server 2012-Anmeldevorgang
In der folgenden Abbildung wird veranschaulicht, wie sich der Anmeldevorgang für einen Administrator vom Anmeldevorgang für einen Standardbenutzer unterscheidet.

![Abbildung, die zeigt, wie sich der Anmeldevorgang für einen Administrator vom Anmeldevorgang für einen Standardbenutzer unterscheidet](../media/How-User-Account-Control-Works/UACWindowsLogonProcess.gif)

Standardmäßig greifen Standardbenutzer und Administratoren auf Ressourcen zu und führen Anwendungen im Sicherheitskontext von Standardbenutzern aus. Wenn sich ein Benutzer an einem Computer anmeldet, erstellt das System einen Zugriffstoken für diesen Benutzer. Das Zugriffstoken beinhaltet Informationen zu den Zugriffsrechten, die dem Benutzer zustehen, einschließlich der Sicherheits-IDs und der Windows-Berechtigungen.

Wenn sich ein Administrator anmeldet, werden für den Benutzer zwei separate Zugriffstoken erstellt: ein Zugriffstoken für Standardbenutzer und ein Zugriffstoken für Administratoren. Das Standardbenutzer-Zugriffstoken enthält dieselben benutzerspezifischen Informationen wie das Administratorzugriffstoken, die Windows-Administratorberechtigungen und SIDs wurden hierbei jedoch entfernt. Das Standardbenutzer Zugriffs Token wird verwendet, um Anwendungen zu starten, die keine administrativen Aufgaben ausführen (Standardbenutzer Anwendungen). Das Standardbenutzer Zugriffs Token wird dann verwendet, um den Desktop (Explorer.exe) anzuzeigen. "Explorer.exe" ist der übergeordnete Prozess, von dem alle anderen vom Benutzer initiierten Prozesse ihre Zugriffstoken erben. Daher werden alle Anwendungen mit Standardbenutzerrechten ausgeführt, sofern ein Benutzer nicht seine Zustimmung erklärt oder seine Anmeldeinformationen angibt, um einer Anwendung die Verwendung eines vollständigen Administratorzugriffstokens zu gestatten.

Ein Benutzer, der ein Mitglied der Gruppe „Administratoren“ ist, kann sich anmelden, im Web surfen und E-Mails lesen, während er ein Standardbenutzer-Zugriffstoken verwendet. Wenn der Administrator einen Task ausführen muss, für den das Administrator Zugriffs Token erforderlich ist, wird der Benutzer von Windows Server 2012 automatisch zur Genehmigung aufgefordert. Diese Eingabeaufforderung wird als Eingabeaufforderung für erhöhte Rechte bezeichnet, und das Verhalten kann mithilfe des Snap-Ins für die lokale Sicherheitsrichtlinie (Secpol.msc) oder der Gruppenrichtlinie konfiguriert werden.

> [!NOTE]
> Der Begriff "Elevate" wird verwendet, um auf den Prozess in Windows Server 2012 zu verweisen, der den Benutzer zur Zustimmung oder zur Eingabe von Anmelde Informationen auffordert, um ein Token für den vollen Administrator Zugriff zu verwenden.

### <a name="the-uac-user-experience"></a>Die UAC-Benutzeroberfläche
Wenn UAC aktiviert ist, unterscheidet sich die Benutzeroberfläche für Standardbenutzer von der für Administratoren im Administratorgenehmigungsmodus. Die empfohlene und sicherere Methode zum Ausführen von Windows Server 2012 besteht darin, Ihr primäres Benutzerkonto als Standardbenutzer Konto zu erstellen. Bei der Ausführung als Standardbenutzer wird die Sicherheit für eine verwaltete Umgebung maximiert. Mit der integrierten UAC-Komponente für erhöhte Rechte können Standardbenutzer einfach eine Verwaltungsaufgabe ausführen, indem sie die gültigen Anmeldeinformationen für ein lokales Administratorkonto eingeben. Bei der standardmäßigen integrierten UAC-Komponente für erhöhte Rechte für Standardbenutzer handelt es sich um die Administratoranmeldeaufforderung.

Die Alternative zur Ausführung als ein Standardbenutzer besteht in der Ausführung als ein Administrator im Administratorgenehmigungsmodus. Mithilfe der integrierten UAC-Komponente für erhöhte Rechte können Mitglieder der lokalen Administratorgruppe einfach eine Verwaltungsaufgabe ausführen, indem Sie die Genehmigung bereitstellen. Die standardmäßige integrierte UAC-Komponente für erhöhte Rechte für ein Administratorkonto im Administratorgenehmigungsmodus wird als Zustimmungsaufforderung bezeichnet. Das UAC-Eingabe Aufforderungs Verhalten für erhöhte Rechte kann mithilfe des Snap-Ins "lokale Sicherheitsrichtlinie" (secpol. msc) oder Gruppenrichtlinie konfiguriert werden.

**Die Zustimmungsaufforderungen und Administratoranmeldeaufforderungen**

Wenn UAC aktiviert ist, werden Sie von Windows Server 2012 zur Zustimmung aufgefordert, oder Sie werden zur Eingabe von Anmelde Informationen eines gültigen lokalen Administrator Kontos aufgefordert, bevor ein Programm oder eine Aufgabe gestartet wird, für die ein vollständiges Administrator Durch diese Aufforderung wird sichergestellt, dass keine Schadsoftware automatisch installiert wird.

**Die Zustimmungsaufforderung**

Die Zustimmungsaufforderung wird angezeigt, wenn ein Benutzer versucht, eine Aufgabe auszuführen, für die das Verwaltungszugriffstoken eines Benutzers erforderlich ist. Im folgenden sehen Sie einen Screenshot der UAC-Zustimmungsaufforderung.

![Screenshot der UAC-Zustimmungsaufforderung](../media/How-User-Account-Control-Works/UACConsentPrompt.gif)

**Die Administratoranmeldeanforderung**

Die Administratoranmeldeanforderung wird angezeigt, wenn ein Standardbenutzer eine Aufgabe ausführen möchte, für die das Administratorzugriffstoken erforderlich ist. Dieses standardmäßige Eingabeaufforderungsverhalten für Standardbenutzer kann mithilfe des Snap-Ins der lokalen Sicherheitsrichtlinie (Secpol.msc) oder der Gruppenrichtlinie konfiguriert werden. Administratoren können auch zur Angabe ihrer Anmeldeinformationen aufgefordert werden, indem der Richtlinieneinstellungswert Benutzerkontensteuerung: Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren im Administratorbestätigungsmodus auf Eingabeaufforderung zu Anmeldeinformationen festgelegt wird.

Der folgende Screenshot zeigt ein Beispiel für die UAC-Eingabeaufforderung für Anmelde Informationen.

![Screenshot mit einem Beispiel für die UAC-Eingabeaufforderung für Anmelde Informationen](../media/How-User-Account-Control-Works/UACCredentialPrompt.gif)

**UAC-Eingabe Aufforderungen**

Die Eingabeaufforderungen für erhöhte Rechte in der Benutzerkontensteuerung besitzen eine Farbcodierung, damit sie bestimmten Anwendungen zugeordnet werden können. Dadurch wird die direkte Identifizierung der potenziellen Sicherheitsrisiken einer Anwendung ermöglicht. Wenn eine Anwendung versucht, mit dem vollständigen Zugriffs Token eines Administrators auszuführen, analysiert Windows Server 2012 zunächst die ausführbare Datei, um deren Verleger zu ermitteln. Anwendungen werden zuerst basierend auf dem Verleger der ausführbaren Datei in drei Kategorien unterteilt: Windows Server 2012, Publisher verifiziert (signiert) und Publisher nicht verifiziert (unsigned). Im folgenden Diagramm wird veranschaulicht, wie Windows Server 2012 die Eingabeaufforderung für die Erhöhung von Farben für den Benutzer festlegt.

Die Farbkodierung für die Eingabeaufforderung für erhöhte Rechte lautet wie folgt:

-   Roter Hintergrund mit einem roten Schildsymbol: Die Anwendung wird von der Gruppenrichtlinie gesperrt, oder sie stammt von einem gesperrten Herausgeber.

-   Blauer Hintergrund mit einem blauen und goldenen Schild Symbol: die Anwendung ist eine Windows Server 2012-Verwaltungs Anwendung, z. b. ein System Steuerungselement.

-   Blauer Hintergrund mit blauem Schildsymbol: Die Anwendung wird mithilfe von Authenticode signiert und wird vom lokalen Computer als vertrauenswürdig eingestuft.

-   Gelber Hintergrund mit gelbem Schildsymbol: Die Anwendung ist nicht signiert oder signiert, doch sie wird vom lokalen Computer nicht als vertrauenswürdig eingestuft.

**Schildsymbol**

Einige Optionen in der Systemsteuerung, zum Beispiel **Datums- und Uhrzeiteigenschaften**, enthalten eine Kombination aus Administrator- und Standardbenutzervorgängen. Standardbenutzer können die Uhrzeit anzeigen und die Zeitzone ändern, doch zum Ändern der lokalen Systemzeit ist ein Token für vollständigen Administratorzugriff erforderlich. Nachfolgend finden Sie einen Screenshot der Systemsteuerungsoption **Datums- und Uhrzeiteigenschaften**.

![Screenshot mit den * * Datums-und Uhrzeit Eigenschaften * * System Steuerungselement](../media/How-User-Account-Control-Works/UACShieldIcon.gif)

Das Schildysmbol auf der Schaltfläche **Datum und Uhrzeit ändern** gibt an, dass der Prozess ein Token für vollständigen Administratoren erfordert. Eine Eingabeaufforderung für erhöhte Rechte der Benutzerkontensteuerung wird angezeigt.

**Sichern der Eingabeaufforderung für erhöhte Rechte**

Die Höherstufung von Rechten wird zusätzlich durch Weiterleiten der Aufforderung an den sicheren Desktop gesichert. Die Eingabe Aufforderungen für Zustimmung und Anmelde Informationen werden standardmäßig auf dem sicheren Desktop unter Windows Server 2012 angezeigt. Nur Windows-Prozesse können auf den sicheren Desktop zugreifen. Ein höheres Sicherheitsniveau erzielen Sie, wenn Sie die Richtlinieneinstellung **Benutzerkontensteuerung: Bei Benutzeraufforderung nach erhöhten Rechten zum sicheren Desktop wechseln** aktiviert lassen.

Wenn eine ausführbare Datei erhöhte Rechte erfordert, wechselt der interaktive Desktop (wird auch als Benutzerdesktop bezeichnet) zum sicheren Desktop. Der sichere Desktop blendet den Benutzerdesktop ab und zeigt eine Eingabeaufforderung für erhöhte Rechte an, die beantwortet werden muss, bevor der Vorgang fortgesetzt werden kann. Wenn der Benutzer auf Ja oder Nein klickt, wechselt der Desktop wieder zurück zum Benutzerdesktop.

Schadsoftware kann eine Imitation des sicheren Desktops darstellen, doch wenn die Richtlinieneinstellung Benutzerkontensteuerung: Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren im Administratorbestätigungsmodus auf Eingabeaufforderung zur Zustimmung festgelegt wurde, erhält die Schadsoftware keine erhöhten Rechte, wenn der Benutzer auf dem imitierten Desktop auf Ja klickt. Wenn die Richtlinieneinstellung auf Eingabeaufforderung zu Anmeldeinformationen festgelegt wird, kann Schadsoftware, die die Administratoranmeldeanforderung imitiert, möglicherweise die Anmeldeinformationen des Benutzers sammeln. Die Schadsoftware erhält jedoch keine erhöhten Rechte, und das System weist andere Schutzmechanismen auf, die verhindern, dass die Schadsoftware die Steuerung der Benutzeroberfläche übernimmt, selbst wenn das Kennwort abgeleitet wird.

Auch wenn Schadsoftware eine Imitation des sicheren Desktops darstellen kann, kann dieses Problem nur dann auftreten, wenn ein Benutzer die Schadsoftware zuvor auf dem Computer installiert hat. Da Prozesse, für die ein Administratorzugriffstoken erforderlich ist, nicht unbeaufsichtigt installiert werden können, wenn die Benutzerkontensteuerung aktiviert ist, muss der Benutzer ausdrücklich seine Zustimmung erklären, indem er auf **Ja** klickt oder Administratoranmeldeinformationen angibt. Die spezifische Verhaltensweise der UAC-Eingabeaufforderung für erhöhte Rechte hängt von „Gruppenrichtlinie“ ab.

## <a name="uac-architecture"></a>UAC-Architektur
Im folgenden Diagramm wird die UAC-Architektur (Architektur der Benutzerkontensteuerung) detailliert dargestellt.

![Diagramm zur UAC-Architektur](../media/How-User-Account-Control-Works/UACArchitecture.gif)

Überprüfen Sie die folgende Tabelle, um die einzelnen Komponenten besser zu verstehen:

|Komponente|BESCHREIBUNG|
|-------|--------|
|**Benutzer**||
|Benutzer führt einen Vorgang aus, für den eine Berechtigung erforderlich ist|Wenn bei dem Vorgang das Dateisystem oder die Registrierung geändert wird, wird die Virtualisierung aufgerufen. Bei allen anderen Vorgängen wird ShellExecute aufgerufen.|
|ShellExecute|ShellExecute ruft CreateProcess auf. ShellExecute sucht nach dem Fehler "ERROR_ELEVATION_REQUIRED" von CreateProcess. Wenn der Fehler empfangen wird, ruft ShellExecute den Anwendungsinformationsdienst auf, um die angeforderte Aufgabe mit der Eingabeaufforderung für erhöhte Rechte auszuführen.|
|CreateProcess|Wenn für die Anwendung eine Erhöhung erforderlich ist, lehnt "kreateprocess" den-Befehl mit ERROR_ELEVATION_REQUIRED ab.|
|**System**||
|Anwendungsinformationsdienst|Ein Systemdienst, der den Start von Anwendungen unterstützt, die zur Ausführung mindestens ein erhöhtes Recht oder Benutzerrecht benötigen (zum Beispiel lokale administrative Aufgaben), sowie von Anwendungen, die höhere Integritätsebenen erfordern. Der Anwendungs Informationsdienst hilft dabei, solche Anwendungen zu starten, indem er einen neuen Prozess für die Anwendung mit dem vollständigen Zugriffs Token eines Administrators erstellt, wenn eine Erhöhung erforderlich ist und (je nach Gruppenrichtlinie) Zustimmung vom Benutzer erteilt wird.|
|Erhöhen einer ActiveX-Installation|Wenn ActiveX nicht installiert ist, überprüft das System die UAC-Schiebereglerstufe. Wenn ActiveX installiert ist, wird die Gruppenrichtlinieneinstellung **Benutzerkontensteuerung: Bei Benutzeraufforderung nach erhöhten Rechten zum sicheren Desktop wechseln** aktiviert.|
|Stufe des UAC-Schiebereglers überprüfen|UAC verfügt jetzt über vier Benachrichtigungs Ebenen, die Sie auswählen können, und einen Schieberegler, mit dem die Benachrichtigungs Ebene ausgewählt wird:<p><ul><li>High<p>    Wenn der Schieberegler auf **Immer benachrichtigen** gerichtet ist, wird vom System überprüft, ob der sichere Desktop aktiviert ist.</li><li>Medium<p>    Wenn der Schieberegler auf **Standard - nur benachrichtigen, wenn Änderungen am Computer von Programmen vorgenommen werden** gerichtet ist, ist die Richtlinieneinstellung **Benutzerkontensteuerung: Nur ausführbare Dateien heraufstufen, die signiert und überprüft sind** aktiviert:<p><ul><li>Wenn die Richtlinien Einstellung aktiviert ist, wird die Überprüfung der PKI-Zertifizierungs Pfade (Public Key-Infrastruktur) für eine bestimmte ausführbare Datei erzwungen, bevor Sie ausgeführt werden darf.</li><li>Wenn die Richtlinieneinstellung nicht aktiviert ist (Standard), wird die Überprüfung des Public Key-Infrastrukturzertifizierungspfads erst erzwungen, wenn eine angegebene ausführbare Datei ausgeführt werden darf. Die Gruppenrichtlinieneinstellung **Benutzerkontensteuerung: Bei Benutzeraufforderung nach erhöhten Rechten zum sicheren Desktop wechseln** ist aktiviert.</li></ul></li><li>Niedrig<p>    Wenn der Schieberegler auf **Nur benachrichtigen, wenn Änderungen am Computer von Programmen vorgenommen werden (Desktop nicht abblenden)** gerichtet ist, wird CreateProcess aufgerufen.</li><li>Nie benachrichtigen<p>    Wenn der Schieberegler auf " **nie Benachrichtigen**" festgelegt ist, wird die UAC-Eingabeaufforderung nie benachrichtigt, wenn ein Programm versucht, eine Änderung auf dem Computer zu installieren oder zu versuchen, eine Änderung vorzunehmen. **Wichtig:**     Diese Einstellung wird nicht empfohlen. Diese Einstellung entspricht dem Festlegen der Richtlinieneinstellung **Benutzerkontensteuerung: Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren im Administratorgenehmigungsmodus** auf **Erhöhte Rechte ohne Eingabeaufforderung**.</li></ul>|
|Aktivierter sicherer Desktop|Die Richtlinieneinstellung **Benutzerkontensteuerung: Bei Benutzeraufforderung nach erhöhten Rechten zum sicheren Desktop wechseln** ist aktiviert:<p>-Wenn der sichere Desktop aktiviert ist, werden alle Anforderungen für erhöhte Rechte unabhängig von den Richtlinien Einstellungen für das Eingabe Aufforderungs Verhalten für Administratoren und Standardbenutzer an den sicheren Desktop gesendet.<br />Wenn der sichere Desktop nicht aktiviert ist, werden alle Anforderungen für erhöhte Rechte an den Desktop des interaktiven Benutzers gesendet, und die benutzerspezifischen Einstellungen für Administratoren und Standardbenutzer werden verwendet.|
|CreateProcess|Von "anateprocess" werden AppCompat-, Fusion-und Installer-Erkennung aufgerufen, um zu bewerten, ob die Anwendung eine Erhöhung Die ausführbare Datei wird anschließend überprüft, um die angeforderte Ausführungsebene zu bestimmen, die im Anwendungsmanifest der ausführbaren Datei gespeichert ist. CreateProcess schlägt fehl, wenn die im Manifest angegebene angeforderte Ausführungsebene nicht dem Zugriffstoken entspricht. In diesem Fall wird ein Fehler (ERROR_ELEVATION_REQUIRED) an ShellExecute zurückgegeben. |
|AppCompat|Die AppCompat-Datenbank speichert Informationen in den Anwendungskompatibilitätspatch-Einträgen für eine Anwendung.|
|Fusion|In der Fusion-Datenbank werden Informationen aus dem Anwendungsmanifesten gespeichert, die die Anwendungen beschreiben. Das Manifestschema wird aktualisiert, um ein Feld für das Hinzufügen einer neuen angeforderten Ausführungsstufe hinzuzufügen.|
|Installationserkennung|Die Installationsprogramm Erkennung erkennt ausführbare Setup Dateien, um zu verhindern, dass Installationen ohne Kenntnis und Zustimmung des Benutzers ausgeführt werden.|
|**Kernel**||
|Virtualisierung|Virtualisierungstechnologie stellt sicher, dass nicht kompatible Anwendungen nicht im Hintergrund ausgeführt werden oder fehlschlagen, wenn die Ursache nicht ermittelt werden kann. UAC bietet zudem eine Datei- und Registrierungsvirtualisierung und Protokollierung für Anwendungen, die in geschützte Bereiche schreiben.|
|Dateisystem und Registrierung|Die benutzerbasierte Datei- und Registrierungsvirtualisierung leitet die Schreibanforderung für die computerbasierte Registrierung und Datei an die entsprechenden benutzerbasierten Speicherorte um. Leseanforderungen werden zuerst an den virtualisierten Einzelbenutzerort und anschließend an den Einzelcomputerort umgeleitet.|

In früheren Windows-Versionen gibt es eine Änderung an Windows Server 2012 UAC. Der neue Schieberegler schaltet die UAC niemals vollständig aus. Die neue Einstellung sieht wie folgt aus:

-   Der UAC-Dienst wird weiterhin ausgeführt.

-   Alle durch Administratoren initiierten Eingabeaufforderungen für erhöhte Rechte werden automatisch genehmigt, ohne dass eine UAC-Eingabeaufforderung angezeigt wird.

-   Für Standardbenutzer werden automatisch alle Eingabeaufforderungen für erhöhte Rechte abgelehnt.

> [!IMPORTANT]
> Zum vollständigen Deaktivieren von UAC müssen Sie die Richtlinie **Benutzerkontensteuerung: Alle Administratoren im Administratorgenehmigungsmodus ausführen**deaktivieren.

> [!WARNING]
> Angepasste Anwendungen können unter Windows Server 2012 nicht verwendet werden, wenn UAC deaktiviert ist.

### <a name="virtualization"></a>Virtualisierung
Da Systemadministratoren in Unternehmensumgebungen Systeme sichern möchten, sind zahlreiche Branchenanwendungen so konzipiert, dass nur ein Zugriffstoken für Standardbenutzer verwendet wird. Dies hat zur Folge, dass IT-Administratoren beim Ausführen von Windows Server 2012 mit aktivierter UAC nicht die Mehrzahl der Anwendungen ersetzen müssen.

 Windows Server 2012 umfasst die Datei-und Registrierungsvirtualisierungstechnologie für Anwendungen, die nicht UAC-kompatibel sind und für die ein Administrator Zugriffs Token erforderlich ist. Durch die Virtualisierung wird sichergestellt, dass selbst Anwendungen, die nicht UAC-kompatibel sind, mit Windows Server 2012 kompatibel sind. Wenn eine administrative Anwendung, die nicht UAC-kompatibel ist, versucht, in ein geschütztes Verzeichnis (z. b. Programmdateien) zu schreiben, gibt die UAC der Anwendung eine eigene virtualisierte Ansicht der Ressource, die Sie zu ändern versucht. Die virtualisierte Kopie wird im Profil des Benutzers verwaltet. Diese Strategie erstellt eine separate Kopie der virtualisierten Datei für jeden Benutzer, der die nicht kompatible Anwendung ausführt.

Die meisten Anwendungsaufgaben werden ordnungsgemäß mithilfe von Virtualisierungsfeatures ausgeführt. Auch wenn die Virtualisierung die Ausführung der meisten Anwendungen zulässt, handelt es sich hierbei um einen kurzfristigen Patch und nicht um eine langfristige Lösung. Anwendungsentwickler sollten Ihre Anwendungen so schnell wie möglich so ändern, dass Sie mit dem Windows Server 2012-Logo Programm kompatibel sind, anstatt sich auf die Virtualisierung von Dateien, Ordnern und Registrierungen verlassen zu müssen.

Virtualisierung ist in den folgenden Szenarien keine Option:

1.  Die Virtualisierung gilt nicht für Anwendungen mit erhöhten Rechten, die mit einem vollen Administrator Zugriffs Token ausgeführt werden.

2.  Virtualisierung unterstützt nur 32-Bit-Anwendungen. 64-Bit-Anwendungen ohne erhöhte Rechte erhalten einfach eine Meldung vom Typ "Zugriff verweigert", wenn Sie versuchen, ein Handle (einen eindeutigen Bezeichner) für ein Windows-Objekt abzurufen. Native Windows 64-Bit-Anwendungen müssen mit UAC kompatibel sein und Daten an die richtigen Speicherorte schreiben.

3.  Die Virtualisierung ist für eine Anwendung deaktiviert, wenn die Anwendung ein Anwendungs Manifest mit einem angeforderten Attribut auf Ausführungs Ebene enthält.

### <a name="request-execution-levels"></a>Anforderungs Ausführungs Ebenen
Ein Anwendungsmanifest ist eine XML-Datei, die die freigegebenen und privaten parallelen Assemblys beschreibt und identifiziert, an die sich eine Anwendung zur Laufzeit binden soll. In Windows Server 2012 enthält das Anwendungs Manifest Einträge für die UAC-Anwendungs Kompatibilität. Administrative Anwendungen, die einen Eintrag im Anwendungs Manifest enthalten, fordern den Benutzer zur Eingabe der Berechtigung für den Zugriff auf das Zugriffs Token des Benutzers auf. Obwohl ihnen ein Eintrag im Anwendungsmanifest fehlt, können die meisten Administratoranwendungen ohne Änderung ausgeführt werden, indem Anwendungskompatibilitätspatches verwendet werden. Anwendungskompatibilitäts-Fixes sind Datenbankeinträge, mit denen Anwendungen, die nicht UAC-kompatibel sind, ordnungsgemäß mit Windows Server 2012 funktionieren.

Allen UAC-kompatiblen Anwendungen muss eine angeforderte Ausführungs Ebene hinzugefügt werden, die dem Anwendungs Manifest hinzugefügt wurde. Wenn die Anwendung Administrator Zugriff auf das System erfordert, stellt das Markieren der Anwendung mit der angeforderten Ausführungs Ebene "Administrator erforderlich" sicher, dass das System dieses Programm als administrative Anwendung identifiziert, und führt die erforderlichen Schritte zur Erhöhung der Rechte aus. Die angeforderten Ausführungsebenen geben die für eine Anwendung erforderlichen Rechte an.

### <a name="installer-detection-technology"></a>Installer-Erkennungstechnologie
Installationsprogramme sind Anwendungen, die zur Bereitstellung von Software entwickelt wurden. Die meisten Installationsprogramme schreiben Daten in Systemverzeichnisse und Registrierungsschlüssel. In diese geschützten Systemspeicherorte kann für gewöhnlich nur ein Administrator oder die Technologie für Installationserkennung schreiben. Somit verfügt ein Standardbenutzer nicht über den benötigten Zugriff, um Programme zu installieren. Windows Server 2012 heuristisch erkennt Installationsprogramme und fordert Administrator Anmelde Informationen oder eine Genehmigung vom Administrator Benutzer an, um mit Zugriffsberechtigungen ausgeführt zu werden. Windows Server 2012 erkennt auch heuristisch Updates und Programme, mit denen Anwendungen deinstalliert werden. Eines der Entwurfsziele für die Benutzerkontensteuerung besteht darin, zu verhindern, dass Installationen ohne das Wissen und die Zustimmung des Benutzers ausgeführt werden, da Installationsprogramme Schreibvorgänge in geschützten Bereichen des Dateisystems und der Registrierung ausführen.

Die Installationserkennung gilt für:

-   Ausführbare 32-Bit-Dateien.

-   Anwendungen ohne Attribut für die angeforderte Ausführungsebene.

-   Interaktive Prozesse, die mit aktivierter UAC als ein Standardbenutzer ausgeführt werden.

Vor dem Erstellen eines 32-Bit-Prozesses werden die folgenden Attribute überprüft, um zu ermitteln, ob sie sich in einem Installer befinden:

-   Der Dateiname enthält Schlüsselwörter wie „install“, „setup“ oder „update“.

-   Felder für Versionsverwaltungsressourcen enthalten die folgenden Schlüsselwörter: Anbieter, Unternehmensname, Produktname, Dateibeschreibung, Ursprünglicher Dateiname, Interner Name und Exportname.

-   Schlüsselwörter im parallelen Manifest werden in die ausführbare Datei eingebettet.

-   Schlüsselwörter in spezifischen „StringTable“-Einträgen werden in der ausführbaren Datei verknüpft.

-   Wichtige Attribute in den Ressourcenskriptdaten werden in der ausführbaren Datei verknüpft.

-   In der ausführbaren Datei befinden sich Zielbytesequenzen.

> [!NOTE]
> Die Schlüsselwörter und Bytesequenzen sind an allgemeine Merkmale angelehnt, die auch in verschiedenen Installationstechnologien zu finden sind.

> [!NOTE]
> Die Richtlinieneinstellung „Benutzerkontensteuerung: Anwendungsinstallationen erkennen und erhöhte Rechte anfordern“ muss für die Installationserkennung aktiviert sein, damit Installationsprogramme erkannt werden können. Diese Einstellung wird standardmäßig aktiviert und kann lokal mithilfe des Snap-Ins für die lokale Sicherheitsrichtlinie (Secpol.msc) oder für die Domäne, OE oder für bestimmte Gruppen nach Gruppenrichtlinie (Gpedit.msc) konfiguriert werden.


