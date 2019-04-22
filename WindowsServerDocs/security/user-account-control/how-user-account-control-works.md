---
title: So funktioniert die Benutzerkontosteuerung
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tpm
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: da83ddb2-6182-417c-aa8e-0b47b2e17d13
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 7f5ad234959ebfe0687b8bc10f9e43f2092252f2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823551"
---
# <a name="how-user-account-control-works"></a>So funktioniert die Benutzerkontosteuerung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Mithilfe der Benutzerkontensteuerung (User Account Control, UAC) können Computer gegen Schäden durch Schadsoftware (auch als "Malware" bezeichnet) geschützt werden, sodass Organisationen besser verwaltete Desktops bereitstellen können. Dank UAC werden Anwendungen und Aufgaben immer im Sicherheitskontext eines Kontos ohne Administratorberechtigungen ausgeführt, es sei denn, ein Administrator autorisiert gezielt Administratorzugriff zum System. UAC kann die automatische Installation von nicht autorisierter Anwendungen blockieren und zu verhindern, dass unbeabsichtigte Änderungen an Systemeinstellungen.

## <a name="uac-process-and-interactions"></a>UAC-Prozess und Interaktionen
Jede Anwendung, die das Administratorzugriffstoken erfordert, muss den Administrator zur Zustimmung auffordern. Die einzige Ausnahme ist die Beziehung, die zwischen den über- und den untergeordneten Prozessen besteht. Untergeordnete Prozesse erben das Zugriffstoken des Benutzers aus dem übergeordneten Prozess an. Allerdings müssen sowohl die über- als auch die untergeordneten Prozesse die gleiche Integritätsebene besitzen. Windows Server 2012 schützt Prozesse durch Markieren der Integritätsebenen. Integritätsebenen geben Aufschluss über die Vertrauenswürdigkeit. Eine Anwendung mit „hoher“ Integrität führt Aufgaben aus, die Systemdaten ändern, beispielsweise eine Anwendung für die Datenträgerpartitionierung. Demgegenüber führt eine Anwendung mit „niedriger“ Integrität Aufgaben aus, die das Betriebssystem potenziell gefährden könnten, beispielsweise ein Webbrowser. Anwendungen mit niedrigerer Integritätsebene können nicht in einer Anwendung mit höherer Integritätsebene ändern. Wenn ein Standardbenutzer versucht, eine Anwendung auszuführen, die ein Administratorzugriffstoken erfordert, erfordert UAC, dass der Benutzer gültige Administratoranmeldeinformationen bereitstellt.

Um besser zu verstehen, wie dieser Prozess findet, dass es wichtig ist, überprüfen die Details des Anmeldevorgangs für Windows Server 2012.

### <a name="windows-server-2012-logon-process"></a>Windows Server 2012-Anmeldevorgang
Die folgende Abbildung zeigt, wie der Anmeldeprozess für einen Administrator vom Anmeldeprozess für einen Standardbenutzer unterscheidet.

![Abbildung veranschaulicht, wie der Anmeldeprozess für einen Administrator vom Anmeldeprozess für einen Standardbenutzer unterscheidet](../media/How-User-Account-Control-Works/UACWindowsLogonProcess.gif)

Standardmäßig greifen Standardbenutzer und Administratoren auf Ressourcen zu und führen Anwendungen im Sicherheitskontext von Standardbenutzern aus. Wenn sich ein Benutzer an einem Computer anmeldet, erstellt das System einen Zugriffstoken für diesen Benutzer. Das Zugriffstoken beinhaltet Informationen zu den Zugriffsrechten, die dem Benutzer zustehen, einschließlich der Sicherheits-IDs und der Windows-Berechtigungen.

Wenn sich ein Administrator anmeldet, werden für den Benutzer zwei separate Zugriffstoken erstellt: ein Zugriffstoken für Standardbenutzer und ein Zugriffstoken für Administratoren. Das Standardbenutzer-Zugriffstoken enthält dieselben benutzerspezifischen Informationen wie das Administratorzugriffstoken, die Windows-Administratorberechtigungen und SIDs wurden hierbei jedoch entfernt. Das Zugriffstoken für Standardbenutzer wird verwendet, zum Starten von Anwendungen, die keine Verwaltungsaufgaben (Anwendungen für Standardbenutzer) durchführen. Das Standardbenutzerzugriffstoken wird dann zum Desktop (Explorer.exe) angezeigt. "Explorer.exe" ist der übergeordnete Prozess, von dem alle anderen vom Benutzer initiierten Prozesse ihre Zugriffstoken erben. Daher werden alle Anwendungen mit Standardbenutzerrechten ausgeführt, sofern ein Benutzer nicht seine Zustimmung erklärt oder seine Anmeldeinformationen angibt, um einer Anwendung die Verwendung eines vollständigen Administratorzugriffstokens zu gestatten.

Ein Benutzer, der ein Mitglied der Gruppe „Administratoren“ ist, kann sich anmelden, im Web surfen und E-Mails lesen, während er ein Standardbenutzer-Zugriffstoken verwendet. Wenn der Administrator muss, um eine Aufgabe auszuführen, die das Administratorzugriffstoken zu Windows Server 2012 automatisch erfordert, wird der Benutzer zur Genehmigung aufgefordert. Diese Eingabeaufforderung wird als Eingabeaufforderung für erhöhte Rechte bezeichnet, und das Verhalten kann mithilfe des Snap-Ins für die lokale Sicherheitsrichtlinie (Secpol.msc) oder der Gruppenrichtlinie konfiguriert werden.

> [!NOTE]
> Der Begriff "erhöhen" werden verwendet, um den Prozess in Windows Server 2012 zu verweisen, die fordert den Benutzer zur Zustimmung oder Anmeldeinformationen für ein Token für vollständigen Administratorzugriff zu verwenden.

### <a name="the-uac-user-experience"></a>Die UAC-Benutzeroberfläche
Wenn UAC aktiviert ist, unterscheidet sich die Benutzeroberfläche für Standardbenutzer von der für Administratoren im Administratorgenehmigungsmodus. Die empfohlene und sicherere Methode der Windows Server 2012 ausgeführt wird, ist Ihr Hauptbenutzerkonto ein Standardbenutzerkonto vornehmen. Bei der Ausführung als Standardbenutzer wird die Sicherheit für eine verwaltete Umgebung maximiert. Mit der integrierten UAC-Komponente für erhöhte Rechte können Standardbenutzer einfach eine Verwaltungsaufgabe ausführen, indem sie die gültigen Anmeldeinformationen für ein lokales Administratorkonto eingeben. Bei der standardmäßigen integrierten UAC-Komponente für erhöhte Rechte für Standardbenutzer handelt es sich um die Administratoranmeldeaufforderung.

Die Alternative zur Ausführung als ein Standardbenutzer besteht in der Ausführung als ein Administrator im Administratorgenehmigungsmodus. Mithilfe der integrierten UAC-Komponente für erhöhte Rechte können Mitglieder der lokalen Administratorgruppe einfach eine Verwaltungsaufgabe ausführen, indem Sie die Genehmigung bereitstellen. Die standardmäßige integrierte UAC-Komponente für erhöhte Rechte für ein Administratorkonto im Administratorgenehmigungsmodus wird als Zustimmungsaufforderung bezeichnet. Das berechtigungserweiterungsverhalten UAC aufgefordert wird, kann mithilfe der Local Security Policy-Snap-in (Secpol.msc) oder der Gruppenrichtlinie konfiguriert werden.

**Die zustimmungs- und administratoranmeldeaufforderungen**

Mit UAC aktiviert ist wird Windows Server 2012 fordert eine Bestätigung oder fordert zur Eingabe von Anmeldeinformationen eines gültigen lokalen Administratorkontos vor dem Starten einer Anwendung oder eine Aufgabe, die ein Token für vollständigen Administratorzugriff erfordert. Durch diese Aufforderung wird sichergestellt, dass keine Schadsoftware automatisch installiert wird.

**Die Zustimmungsaufforderung**

Die Zustimmungsaufforderung wird angezeigt, wenn ein Benutzer versucht, eine Aufgabe auszuführen, für die das Verwaltungszugriffstoken eines Benutzers erforderlich ist. Folgendes ist ein Screenshot, der die UAC-zustimmungsaufforderung.

![Screenshot der UAC-zustimmungsaufforderung](../media/How-User-Account-Control-Works/UACConsentPrompt.gif)

**Die Administratoranmeldeanforderung**

Die Administratoranmeldeanforderung wird angezeigt, wenn ein Standardbenutzer eine Aufgabe ausführen möchte, für die das Administratorzugriffstoken erforderlich ist. Dieses standardmäßige Eingabeaufforderungsverhalten für Standardbenutzer kann mithilfe des Snap-Ins der lokalen Sicherheitsrichtlinie (Secpol.msc) oder der Gruppenrichtlinie konfiguriert werden. Administratoren können auch aufgefordert, ihre Anmeldeinformationen einzugeben, durch Festlegen der User Account Control: Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren im Administratorbestätigungsmodus Richtlinie Einstellungswert auf Aufforderung zur Eingabe von Anmeldeinformationen.

Im folgenden Screenshot ist ein Beispiel für die UAC-administratoranmeldeaufforderung.

![Screenshot zeigt ein Beispiel für die UAC-administratoranmeldeaufforderung](../media/How-User-Account-Control-Works/UACCredentialPrompt.gif)

**UAC-eingabeaufforderungen für erhöhte Rechte**

Die Eingabeaufforderungen für erhöhte Rechte in der Benutzerkontensteuerung besitzen eine Farbcodierung, damit sie bestimmten Anwendungen zugeordnet werden können. Dadurch wird die direkte Identifizierung der potenziellen Sicherheitsrisiken einer Anwendung ermöglicht. Wenn eine Anwendung versucht, die mit dem vollzugriffstoken eines Administrators ausgeführt werden, analysiert Windows Server 2012 zuerst die ausführbare Datei aus, um den Herausgeber zu ermitteln. Anwendungen werden zuerst basierend auf dem Verleger für die ausführbare Datei in drei Kategorien unterteilt:  WindowsServer 2012 "," Herausgeber überprüft (signiert) und Herausgeber nicht überprüft (ohne Vorzeichen). Das folgende Diagramm veranschaulicht, wie Windows Server 2012 ermittelt, welche Farbe Eingabeaufforderung für erhöhte Rechte, die dem Benutzer angezeigt wird.

Die Farbkodierung für die Eingabeaufforderung für erhöhte Rechte lautet wie folgt:

-   Roter Hintergrund mit einem roten Schildsymbol: Die Anwendung, die von der Gruppenrichtlinie gesperrt ist oder von einem Verleger, der blockiert ist.

-   Blauer Hintergrund mit einem blauen und einem goldfarbenen Schildsymbol: Die Anwendung ist eine Windows Server 2012-verwaltungsanwendung, wie z. B. die Elemente der Systemsteuerung.

-   Blauer Hintergrund mit blauem Schildsymbol: Die Anwendung mit Authenticode signiert ist und von dem lokalen Computer als vertrauenswürdig eingestuft wird.

-   Gelber Hintergrund mit gelbem Schildsymbol: Die Anwendung ist nicht signiert oder signiert, aber noch nicht vom lokalen Computer vertrauenswürdig ist.

**Schildsymbol**

Einige Optionen in der Systemsteuerung, zum Beispiel **Datums- und Uhrzeiteigenschaften**, enthalten eine Kombination aus Administrator- und Standardbenutzervorgängen. Standardbenutzer können die Uhrzeit anzeigen und die Zeitzone ändern, doch zum Ändern der lokalen Systemzeit ist ein Token für vollständigen Administratorzugriff erforderlich. Nachfolgend finden Sie einen Screenshot der Systemsteuerungsoption **Datums- und Uhrzeiteigenschaften**.

![Screenshot mit der ** Datum und Uhrzeit Eigenschaften ** Control Panel-Element](../media/How-User-Account-Control-Works/UACShieldIcon.gif)

Das Schildysmbol auf der Schaltfläche **Datum und Uhrzeit ändern** gibt an, dass der Prozess ein Token für vollständigen Administratoren erfordert. Eine Eingabeaufforderung für erhöhte Rechte der Benutzerkontensteuerung wird angezeigt.

**Sichern die Eingabeaufforderung für erhöhte Rechte**

Die Höherstufung von Rechten wird zusätzlich durch Weiterleiten der Aufforderung an den sicheren Desktop gesichert. Die zustimmungs- und administratoranmeldeaufforderungen werden standardmäßig in Windows Server 2012 auf dem sicheren Desktop angezeigt. Nur Windows-Prozesse können auf den sicheren Desktop zugreifen. Für höhere Sicherheit, empfehlen wir unter Beibehaltung der **User Account Control: Wechseln Sie bei benutzeraufforderung nach erhöhten Rechten zum sicheren Desktop** aktivierte richtlinieneinstellung.

Wenn eine ausführbare Datei erhöhte Rechte erfordert, wechselt der interaktive Desktop (wird auch als Benutzerdesktop bezeichnet) zum sicheren Desktop. Der sichere Desktop blendet den Benutzerdesktop ab und zeigt eine Eingabeaufforderung für erhöhte Rechte an, die beantwortet werden muss, bevor der Vorgang fortgesetzt werden kann. Wenn der Benutzer klickt auf Ja oder Nein, wechselt der Desktop zum Benutzerdesktop zurück.

Schadsoftware kann eine Imitation des sicheren Desktops, aber wenn das Benutzerkonto steuern: Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren im Administratorbestätigungsmodus richtlinieneinstellung eine Eingabeaufforderung zur Zustimmung festgelegt ist, wird die Malware keine Erhöhung der Rechte erhalten Wenn der Benutzer klickt auf "" zu klicken Ja. Wenn die richtlinieneinstellung auf Aufforderung zur Eingabe von Anmeldeinformationen festgelegt ist, kann Malware, die die administratoranmeldeanforderung die Anmeldeinformationen des Benutzers erfassen können. Die Schadsoftware erhält jedoch keine erhöhten Rechte, und das System weist andere Schutzmechanismen auf, die verhindern, dass die Schadsoftware die Steuerung der Benutzeroberfläche übernimmt, selbst wenn das Kennwort abgeleitet wird.

Auch wenn Schadsoftware eine Imitation des sicheren Desktops darstellen kann, kann dieses Problem nur dann auftreten, wenn ein Benutzer die Schadsoftware zuvor auf dem Computer installiert hat. Da Prozesse, für die ein Administratorzugriffstoken erforderlich ist, nicht unbeaufsichtigt installiert werden können, wenn die Benutzerkontensteuerung aktiviert ist, muss der Benutzer ausdrücklich seine Zustimmung erklären, indem er auf **Ja** klickt oder Administratoranmeldeinformationen angibt. Die spezifische Verhaltensweise der UAC-Eingabeaufforderung für erhöhte Rechte hängt von „Gruppenrichtlinie“ ab.

## <a name="uac-architecture"></a>UAC-Architektur
Im folgenden Diagramm wird die UAC-Architektur (Architektur der Benutzerkontensteuerung) detailliert dargestellt.

![Diagramm mit der UAC-Architektur](../media/How-User-Account-Control-Works/UACArchitecture.gif)

Zum besseren Verständnis der einzelnen Komponenten finden Informationen Sie in der folgenden Tabelle:

|Component|Beschreibung|
|-------|--------|
|**User**||
|Benutzer führt einen Vorgang aus, für den eine Berechtigung erforderlich ist|Wenn bei dem Vorgang das Dateisystem oder die Registrierung geändert wird, wird die Virtualisierung aufgerufen. Bei allen anderen Vorgängen wird ShellExecute aufgerufen.|
|ShellExecute|ShellExecute ruft CreateProcess auf. ShellExecute sucht nach dem Fehler "ERROR_ELEVATION_REQUIRED" von CreateProcess. Wenn der Fehler empfangen wird, ruft ShellExecute den Anwendungsinformationsdienst auf, um die angeforderte Aufgabe mit der Eingabeaufforderung für erhöhte Rechte auszuführen.|
|CreateProcess|Wenn die Anwendung erhöhte Rechte erforderlich ist, lehnt CreateProcess den Aufruf mit ERROR_ELEVATION_REQUIRED ab.|
|**System**||
|Anwendungsinformationsdienst|Ein Systemdienst, der den Start von Anwendungen unterstützt, die zur Ausführung mindestens ein erhöhtes Recht oder Benutzerrecht benötigen (zum Beispiel lokale administrative Aufgaben), sowie von Anwendungen, die höhere Integritätsebenen erfordern. Vom Benutzer erhält die Anwendungsinformationen Service hilft starten solcher Anwendungen, indem Sie einen neuen Prozess für die Anwendung mit vollen Zugriffstoken ein Administrator erstellt werden, wenn erhöhte Rechte erforderlich sind und (je nach Gruppenrichtlinie) zustimmen dazu.|
|Erhöhen einer ActiveX-Installation|Wenn ActiveX nicht installiert ist, überprüft das System die UAC-Schiebereglerstufe. Wenn ActiveX installiert ist, die **User Account Control: Wechseln Sie bei benutzeraufforderung nach erhöhten Rechten zum sicheren Desktop** Einstellung der Gruppenrichtlinie aktiviert ist.|
|Stufe des UAC-Schiebereglers überprüfen|UAC verfügt jetzt über vier Ebenen der Benachrichtigung auswählen und einen Schieberegler zu verwenden, um die Benachrichtigungsebene auszuwählen:<br /><br /><ul><li>Hoch<br /><br />    Wenn der Schieberegler auf **Immer benachrichtigen** gerichtet ist, wird vom System überprüft, ob der sichere Desktop aktiviert ist.</li><li>Mittel<br /><br />    Wenn der Schieberegler, um festgelegt ist **Standard-benachrichtigen mich nur, wenn Programme versuchen, Änderungen an meinem Computer vornehmen**, **User Account Control: Erhöhte Rechte nur für ausführbare Dateien, die signiert und überprüft sind** richtlinieneinstellung aktiviert ist:<br /><br /><ul><li>Wenn die richtlinieneinstellung aktiviert ist, wird der public Key-Infrastruktur (PKI)-zertifizierungspfadüberprüfung für eine angegebene ausführbare Datei erzwungen, bevor es ausgeführt werden darf.</li><li>Wenn die Richtlinieneinstellung nicht aktiviert ist (Standard), wird die Überprüfung des Public Key-Infrastrukturzertifizierungspfads erst erzwungen, wenn eine angegebene ausführbare Datei ausgeführt werden darf. Die Richtlinieneinstellung **Benutzerkontensteuerung: Wechseln Sie bei benutzeraufforderung nach erhöhten Rechten zum sicheren Desktop** Einstellung der Gruppenrichtlinie aktiviert ist.</li></ul></li><li>Niedrig<br /><br />    Wenn der Schieberegler auf **Nur benachrichtigen, wenn Änderungen am Computer von Programmen vorgenommen werden (Desktop nicht abblenden)** gerichtet ist, wird CreateProcess aufgerufen.</li><li>Nie benachrichtigen<br /><br />    Wenn der Schieberegler, um festgelegt ist **nie benachrichtigen bei**, UAC-Eingabeaufforderung wird nie benachrichtigen, wenn ein Programm installieren möchten oder auf dem Computer keine Änderungen vornehmen möchten. **Wichtig:**     Diese Einstellung wird nicht empfohlen. Diese Einstellung ist identisch mit dem Festlegen der **User Account Control: Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren im Administratorbestätigungsmodus** richtlinieneinstellung, um **erhöhte Rechte ohne Eingabeaufforderung**.</li></ul>|
|Aktivierter sicherer Desktop|Die Richtlinieneinstellung **Benutzerkontensteuerung: Wechseln Sie bei benutzeraufforderung nach erhöhten Rechten zum sicheren Desktop** richtlinieneinstellung aktiviert ist:<br /><br />– Wenn der sichere Desktop aktiviert ist, wechseln Sie zum sicheren Desktop unabhängig von Einstellungen für das Verhalten der Eingabeaufforderung für Administratoren und Standardbenutzer alle Anforderungen für erhöhte Rechte.<br />– Wenn der sichere Desktop nicht aktiviert ist, werden alle Anforderungen für erhöhte Rechte wechseln, auf dem interaktiven Desktop des Benutzers, und die einzelbenutzereinstellungen für Administratoren und Standardbenutzer verwendet werden.|
|CreateProcess|CreateProcess ruft AppCompat, Fusion und Installer-Erkennung zu bewerten, ob die Anwendung erhöhte Rechte erforderlich sind. Die ausführbare Datei wird anschließend überprüft, um die angeforderte Ausführungsebene zu bestimmen, die im Anwendungsmanifest der ausführbaren Datei gespeichert ist. CreateProcess schlägt fehl, wenn die im Manifest angegebene angeforderte Ausführungsebene nicht dem Zugriffstoken entspricht. In diesem Fall wird ein Fehler (ERROR_ELEVATION_REQUIRED) an ShellExecute zurückgegeben. |
|AppCompat|Die AppCompat-Datenbank speichert Informationen in den Anwendungskompatibilitätspatch-Einträgen für eine Anwendung.|
|Fusion|In der Fusion-Datenbank werden Informationen aus dem Anwendungsmanifesten gespeichert, die die Anwendungen beschreiben. Das Manifestschema wird aktualisiert, um ein Feld für das Hinzufügen einer neuen angeforderten Ausführungsstufe hinzuzufügen.|
|Installationserkennung|Die Installererkennung entdeckt ausführbare Setupdateien, was dabei hilft zu verhindern, dass Installationen ohne Kenntnis und Zustimmung des Benutzers ausgeführt werden.|
|**Kernel**||
|Virtualisierung|Virtualisierungstechnologie stellt sicher, dass nicht kompatible Anwendungen nicht ohne Meldung fehl, führen Sie zum Ausführen oder in einer Weise, dass die Ursache nicht bestimmt werden kann fehlschlagen. UAC bietet zudem eine Datei- und Registrierungsvirtualisierung und Protokollierung für Anwendungen, die in geschützte Bereiche schreiben.|
|Dateisystem und Registrierung|Die benutzerbasierte Datei- und Registrierungsvirtualisierung leitet die Schreibanforderung für die computerbasierte Registrierung und Datei an die entsprechenden benutzerbasierten Speicherorte um. Leseanforderungen werden zuerst an den virtualisierten Einzelbenutzerort und anschließend an den Einzelcomputerort umgeleitet.|

Von früheren Windows-Versionen zu Windows Server 2012 UAC geändert wird. Der neue Schieberegler wird nie UAC vollständig zu deaktivieren. Die neue Einstellung führt Folgendes aus:

-   Der UAC-Dienst wird weiterhin ausgeführt.

-   Alle durch Administratoren initiierten Eingabeaufforderungen für erhöhte Rechte werden automatisch genehmigt, ohne dass eine UAC-Eingabeaufforderung angezeigt wird.

-   Für Standardbenutzer werden automatisch alle Eingabeaufforderungen für erhöhte Rechte abgelehnt.

> [!IMPORTANT]
> Um vollständig UAC zu deaktivieren. deaktivieren Sie die Richtlinie **User Account Control: Alle Administratoren im Administratorbestätigungsmodus ausführen**.

> [!WARNING]
> Maßgeschneiderte Anwendungen funktionieren nicht unter Windows Server 2012, wenn UAC deaktiviert ist.

### <a name="virtualization"></a>Virtualisierung
Da Systemadministratoren in Unternehmensumgebungen Systeme sichern möchten, sind zahlreiche Branchenanwendungen so konzipiert, dass nur ein Zugriffstoken für Standardbenutzer verwendet wird. Daher müssen IT-Administratoren nicht die Mehrheit der Anwendungen zu ersetzen, wenn Sie Windows Server 2012 mit aktivierter UAC ausführen.

 Windows Server 2012 enthält Datei- und Virtualisierungstechnologie für Anwendungen, die nicht UAC-kompatibel sind und für die ordnungsgemäße Ausführung ein Administratorzugriffstoken erfordern. Virtualisierung stellt sicher, dass sogar Anwendungen, die nicht UAC-kompatibel sind mit Windows Server 2012 kompatibel sind. Wenn eine administrative Anwendung, die nicht UAC-kompatible versucht wird, zum Schreiben in ein geschütztes Verzeichnis wie z. B. Programme, liefert UAC der Anwendung ihre eigene virtualisierte Ansicht der Ressource, die sie gerade ändern. Die virtualisierte Kopie wird im Profil des Benutzers verwaltet. Diese Strategie erstellt eine separate Kopie der virtualisierten Datei für jeden Benutzer, die die nicht kompatible Anwendung ausgeführt wird.

Die meisten Anwendungsaufgaben werden ordnungsgemäß mithilfe von Virtualisierungsfeatures ausgeführt. Auch wenn die Virtualisierung die Ausführung der meisten Anwendungen zulässt, handelt es sich hierbei um einen kurzfristigen Patch und nicht um eine langfristige Lösung. Anwendungsentwickler sollten ihre Anwendungen mit dem Windows Server 2012-Logo-Programm so bald wie möglich kompatibel, anstatt auf Datei-, Ordner- und Registrierung der vertrauenden Seite ändern.

Virtualisierung ist in den folgenden Szenarien keine Option:

1.  Virtualisierung gilt nicht für Anwendungen, die erhöhte und mit einem Token für vollen Administratorzugriff ausgeführt werden.

2.  Virtualisierung unterstützt nur 32-Bit-Anwendungen. Erhöhte Rechte nicht 64-Bit-Anwendungen erhalten einfach "Zugriff verweigert" angezeigt, wenn sie versuchen, ein Handle (Eindeutiger Bezeichner) für eine Windows-Objekt abzurufen. Systemeigene Windows-64-Bit-Anwendungen müssen mit UAC kompatibel und Daten an die richtigen Standorte schreiben.

3.  Virtualisierung ist für eine Anwendung deaktiviert, wenn die Anwendung ein Anwendungsmanifest mit einem Attribut für eine angeforderte Ausführungsebene enthält.

### <a name="request-execution-levels"></a>Anforderung Ausführungsebenen
Ein Anwendungsmanifest ist eine XML-Datei, die die freigegebenen und privaten parallelen Assemblys, mit denen eine Anwendung eine Bindung erstellen soll, beschreibt und identifiziert. In Windows Server 2012 enthält das Anwendungsmanifest Einträge für Zwecke der UAC-Anwendungskompatibilität. Administrative Anwendungen, die einen Eintrag im Anwendungsmanifest enthalten auffordern den Benutzer für die Berechtigung zum Zugriffstoken des Benutzers zugreifen. Obwohl ihnen ein Eintrag im Anwendungsmanifest fehlt, können die meisten Administratoranwendungen ohne Änderung ausgeführt werden, indem Anwendungskompatibilitätspatches verwendet werden. Anwendungskompatibilitätspatches sind Datenbankeinträge, die Anwendungen zu ermöglichen, die nicht UAC-kompatibel mit Windows Server 2012 ordnungsgemäß funktioniert.

Alle UAC-kompatible Anwendungen benötigen eine angeforderte Ausführungsebene zum Anwendungsmanifest hinzugefügt. Wenn die Anwendung erfordert Administratorzugriff auf das System, markieren die Anwendung mit einer angeforderten Ausführungsebene "Administrator erforderlich" wird sichergestellt, dass das System dieses Programm als administrative Anwendung identifiziert und führt die notwendigen Erhöhungsschritte. Die angeforderten Ausführungsebenen geben die für eine Anwendung erforderlichen Rechte an.

### <a name="installer-detection-technology"></a>Technologie zur Installationsprogrammerkennung
Installationsprogramme sind Anwendungen, die zum Bereitstellen von Software entwickelt. Die meisten Installationsprogramme schreiben Daten in Systemverzeichnisse und Registrierungsschlüssel. In diese geschützten Systemspeicherorte kann für gewöhnlich nur ein Administrator oder die Technologie für Installationserkennung schreiben. Somit verfügt ein Standardbenutzer nicht über den benötigten Zugriff, um Programme zu installieren. Windows Server 2012 eine heuristische Erkennung Installationsprogramme und fordert Administratoranmeldeinformationen oder Genehmigung durch den Administrator, um mit Zugriffsberechtigungen auszuführen. Windows Server 2012 erkennt heuristisch auch Aktualisierungs-, Updates und Programmen, die Anwendungen zu deinstallieren. Eines der Entwurfsziele für die Benutzerkontensteuerung besteht darin, zu verhindern, dass Installationen ohne das Wissen und die Zustimmung des Benutzers ausgeführt werden, da Installationsprogramme Schreibvorgänge in geschützten Bereichen des Dateisystems und der Registrierung ausführen.

Die Installationserkennung gilt für:

-   Ausführbare 32-Bit-Dateien.

-   Anwendungen ohne Attribut für die angeforderte Ausführungsebene.

-   Interaktive Prozesse, die mit aktivierter UAC als ein Standardbenutzer ausgeführt werden.

Vor dem Erstellen eines 32-Bit-Prozesses werden die folgenden Attribute überprüft, um zu ermitteln, ob sie sich in einem Installer befinden:

-   Der Dateiname enthält Schlüsselwörter wie „install“, „setup“ oder „update“.

-   Felder für versionsverwaltungsressourcen enthalten die folgenden Schlüsselwörter: Anbieter, Firmenname, Produktname, DateiBeschreibung, Ursprünglicher Dateiname, interner Name und exportname.

-   Schlüsselwörter im parallelen Manifest werden in die ausführbare Datei eingebettet.

-   Schlüsselwörter in spezifischen „StringTable“-Einträgen werden in der ausführbaren Datei verknüpft.

-   Wichtige Attribute in den Ressourcenskriptdaten werden in der ausführbaren Datei verknüpft.

-   In der ausführbaren Datei befinden sich Zielbytesequenzen.

> [!NOTE]
> Die Schlüsselwörter und Bytesequenzen sind an allgemeine Merkmale angelehnt, die auch in verschiedenen Installationstechnologien zu finden sind.

> [!NOTE]
> Die Benutzerkontensteuerung: Anwendungsinstallationen erkennen und die Eingabeaufforderung für erhöhte Rechte für die installationsprogrammerkennung Installationsprogramme erkennen aktiviert werden muss. Diese Einstellung wird standardmäßig aktiviert und kann lokal mithilfe des Snap-Ins für die lokale Sicherheitsrichtlinie (Secpol.msc) oder für die Domäne, OE oder für bestimmte Gruppen nach Gruppenrichtlinie (Gpedit.msc) konfiguriert werden.


