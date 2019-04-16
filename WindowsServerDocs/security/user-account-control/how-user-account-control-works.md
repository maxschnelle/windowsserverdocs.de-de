---
title: Funktionsweise der Benutzerkontensteuerung
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
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="how-user-account-control-works"></a>Funktionsweise der Benutzerkontensteuerung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Benutzerkontensteuerung (UAC) verhindert, dass Schadsoftware (auch Malware genannt) von einem Computer zu beschädigen und unterstützt Unternehmen bei einer besser verwalteten desktopumgebung. Mit der Benutzerkontensteuerung ausgeführt Anwendungen und Aufgaben immer im Sicherheitskontext eines Kontos ohne Administratorrechte, wenn ein Administrator ausdrücklich Zugriff auf Administratorebene auf das System autorisiert. UAC können Sie die automatische Installation von nicht autorisierten Anwendungen blockieren und unbeabsichtigte Änderungen an Systemeinstellungen verhindern.

## <a name="uac-process-and-interactions"></a>UAC-Prozess und Interaktionen
Jede Anwendung, die das Administratorzugriffstoken erforderlich ist, muss den Administrator zur Zustimmung auffordern. Die einzige Ausnahme ist die Beziehung, die zwischen übergeordneten und untergeordneten Prozessen besteht. Untergeordnete Prozesse erben das Zugriffstoken des Benutzers vom übergeordneten Prozess. Die über- und untergeordnete Prozesse, müssen jedoch die gleiche Integritätsebene besitzen. Windows Server 2012 schützt Prozesse durch Markieren der Integritätsebenen. Integritätsebenen geben Aufschluss über die Vertrauenswürdigkeit. Eine Anwendung "hoher" Integrität ist eine, die Aufgaben ausführt, die Systemdaten ändern, z. B. einen Datenträger partitioniert Anwendung, während eine "niedriger" Integrität-Anwendung ist, die Aufgaben ausführt, die das Betriebssystem, beispielsweise ein Webbrowser potenziell gefährden könnten. Anwendungen mit niedriger Integrität können Daten in Anwendungen mit höheren Integritätsstufen nicht ändern. Wenn ein Standardbenutzer versucht, eine Anwendung ausgeführt werden, die ein Administratorzugriffstoken erforderlich ist, erfordert UAC, dass der Benutzer gültige Administratoranmeldeinformationen angibt.

Um besser zu verstehen, wie dieser Prozess erfolgt, ist es wichtig, die Details des Anmeldevorgangs Windows Server 2012 zu überprüfen.

### <a name="windows-server-2012-logon-process"></a>Windows Server 2012-Anmeldevorgang
Die folgende Abbildung zeigt, wie der Anmeldeprozess für einen Administrator vom Anmeldeprozess für einen Standardbenutzer unterscheidet.

![Abbildung zur Veranschaulichung, wie der Anmeldeprozess für einen Administrator vom Anmeldeprozess für einen Standardbenutzer unterscheidet sich](../media/How-User-Account-Control-Works/UACWindowsLogonProcess.gif)

Standardmäßig werden Standardbenutzer und Administratoren den Zugriff auf Ressourcen und Anwendungen im Sicherheitskontext von Standardbenutzern ausführen. Wenn ein Benutzer an einem Computer anmeldet, erstellt das System ein Zugriffstoken für den Benutzer. Das Zugriffstoken enthält Informationen über die Zugriffsebene, die der Benutzer zustehen, einschließlich der Sicherheits-IDs (SIDs) und Windows-Berechtigungen.

Wenn ein Administrator anmeldet, werden für den Benutzer zwei separate Zugriffstoken erstellt: ein Zugriffstoken für Standardbenutzer und ein Administratorzugriffstoken. Das Standardbenutzer-Zugriffstoken enthält dieselbe benutzerspezifischen Informationen wie das Administratorzugriffstoken, aber die Windows-Administratorberechtigungen und SIDs wurden entfernt. Zum Starten von Anwendungen, die keine administrative Aufgaben (standard User Applications) ausführen, wird das Zugriffstoken für Standardbenutzer verwendet. Das Standardbenutzer-Zugriffstoken wird dann verwendet, um den Desktop (Explorer.exe) angezeigt. Explorer.exe ist der übergeordnete Prozess, von dem alle anderen Benutzer initiierten Prozesse ihre Zugriffstoken erben. Daher ausführen alle Anwendungen als Standardbenutzer, es sei denn, ein Benutzer seine Zustimmung erklärt oder Anmeldeinformationen, um eine Anwendung mit einem Token für vollen Administratorzugriff zu genehmigen.

Ein Benutzer, der ein Mitglied der Gruppe "Administratoren" ist kann melden Sie sich im Internet surfen und e-Mails lesen und ein Zugriffstoken für Standardbenutzer verwenden. Wenn der Administrator muss eine Aufgabe ausführen, die das Administratorzugriffstoken, Windows Server 2012 automatisch erforderlich ist, fordert den Benutzer zur Genehmigung. Diese Aufforderung wird eine Eingabeaufforderung für erhöhte Rechte bezeichnet, und sein Verhalten kann mithilfe der lokalen Sicherheitsrichtlinien-Snap-in (Secpol.msc) oder der Gruppenrichtlinie konfiguriert werden.

> [!NOTE]
> Der Begriff "heraufstufen" werden verwendet, den Prozess in Windows Server 2012 zu verweisen, die mit der Aufforderung zur Zustimmung oder Anmeldeinformationen um ein Token für vollständigen Administratorzugriff zu verwenden.

### <a name="the-uac-user-experience"></a>Die UAC-Benutzeroberfläche
Wenn UAC aktiviert ist, wird die Benutzeroberfläche für Standardbenutzer unterscheidet, von Administratoren im Administratorgenehmigungsmodus. Die empfohlene und sicherere Methode der Windows Server 2012 ausgeführt wird, stellen Sie Ihr primäre Benutzerkonto in ein Standardbenutzerkonto. Ausführung als Standardbenutzer wird die Sicherheit für eine verwaltete Umgebung maximiert. Mit der integrierten UAC für erhöhte Rechte Komponente können Standardbenutzer einfach eine Verwaltungsaufgabe ausführen, gültige Anmeldeinformationen für ein lokales Administratorkonto eingeben. Die standardmäßige integrierte UAC-Komponente für erhöhte Rechte für Standardbenutzer wird die administratoranmeldeaufforderung.

Die Alternative zur Ausführung als Standardbenutzer wird als Administrator im Administratorbestätigungsmodus ausführen. Mit der integrierten UAC für erhöhte Rechte Komponente können Mitglieder der lokalen Gruppe Administratoren problemlos eine administrative Aufgabe ausführen, durch Erteilen einer Genehmigung. Der Standardwert ist integrierten UAC-Komponente für erhöhte Rechte für ein Administratorkonto im Administratorgenehmigungsmodus wird als zustimmungsaufforderung bezeichnet. Die UAC für erhöhte Rechte Abfrage Verhalten kann mithilfe der lokalen Sicherheitsrichtlinien-Snap-in (Secpol.msc) oder der Gruppenrichtlinie konfiguriert werden.

**Die zustimmungsaufforderungen und administratoranmeldeaufforderungen**

Bei aktivierter UAC Windows Server 2012 zur Zustimmung aufgefordert werden oder die Angabe von Anmeldeinformationen eines gültigen lokalen Administratorkontos vor dem Starten, ein Programm oder eine Aufgabe, die ein Token für vollständigen Administratorzugriff erfordert. Diese Aufforderung wird sichergestellt, dass keine Schadsoftware automatisch installiert werden kann.

**Die Aufforderung zur Zustimmung**

Die zustimmungsaufforderung wird angezeigt, wenn ein Benutzer versucht, eine Aufgabe auszuführen, die Administratorzugriffstoken eines Benutzers erforderlich ist. Im folgenden finden einen Screenshot der UAC-zustimmungsaufforderung.

![Screenshot der UAC-zustimmungsaufforderung](../media/How-User-Account-Control-Works/UACConsentPrompt.gif)

**Die administratoranmeldeanforderung**

Die administratoranmeldeanforderung wird angezeigt, wenn ein Standardbenutzer versucht, eine Aufgabe auszuführen, die Administratorzugriffstoken eines Benutzers erforderlich ist. Dieses standardmäßige eingabeaufforderungsverhalten kann mithilfe der lokalen Sicherheitsrichtlinien-Snap-in (Secpol.msc) oder der Gruppenrichtlinie konfiguriert werden. Administratoren können auch erforderlich, um ihre Anmeldeinformationen einzugeben, durch Festlegen der Benutzerkontensteuerung: Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren im Administratorbestätigungsmodus richtlinieneinstellung Wert auf Aufforderung zur Eingabe von Anmeldeinformationen.

Im folgenden Screenshot ist ein Beispiel für die UAC-administratoranmeldeaufforderung.

![Screenshot mit der ein Beispiel für die UAC-administratoranmeldeaufforderung](../media/How-User-Account-Control-Works/UACCredentialPrompt.gif)

**UAC-eingabeaufforderungen**

Die UAC-eingabeaufforderungen für erhöhte Rechte sind farbkodiert Anwendung spezifisch, wodurch die direkte Identifizierung der potenzielles Sicherheitsrisiko einer Anwendung sein. Wenn eine Anwendung versucht, mit dem vollständigen Zugriffstoken eines Administrators ausgeführt, analysiert Windows Server 2012 zunächst die ausführbare Datei, um den Herausgeber zu bestimmen. Anwendungen werden zuerst in drei Kategorien basierend auf die ausführbare Datei Herausgeber getrennt: WindowsServer 2012, Herausgeber überprüft (signiert) und nicht vom Herausgeber überprüfte (nicht signierte). Das folgende Diagramm zeigt, wie Windows Server 2012 Eingabeaufforderung für erhöhte Rechte der Farbe der Benutzer bestimmt.

Die erhöhte Rechte farbkodierung für die Eingabeaufforderung lautet wie folgt:

-   Roter Hintergrund mit einem roten Schildsymbol: die Anwendung wird durch eine Gruppenrichtlinie blockiert oder stammt von einem Herausgeber, die blockiert wird.

-   Blauer Hintergrund mit einem blauen und goldenen Schildsymbol: die Anwendung wird von Windows Server 2012 administrative, z. B. ein Element der Systemsteuerung.

-   Blauer Hintergrund mit blauem Schildsymbol: die Anwendung wird mithilfe von Authenticode signiert und wird vom lokalen Computer als vertrauenswürdig eingestuft.

-   Gelber Hintergrund mit gelbem Schildsymbol: die Anwendung nicht signiert oder signiert ist, aber noch nicht vom lokalen Computer vertrauenswürdig ist.

**Schildsymbol**

Einige der Systemsteuerung Elemente, z. B. **Datums- und Uhrzeiteigenschaften**, enthalten eine Kombination aus Administrator- und Standardbenutzervorgängen. Standardbenutzer können die Uhrzeit anzeigen und Ändern der Zeitzone, aber ein Token für vollständigen Administratorzugriff ist erforderlich, um die lokale Systemzeit zu ändern. Im folgenden finden Sie einen Screenshot der **Datums- und Uhrzeiteigenschaften** in der Systemsteuerung.

![Screenshot mit dem ** Element für Datum und Uhrzeit Eigenschaften ** der Systemsteuerung](../media/How-User-Account-Control-Works/UACShieldIcon.gif)

Das schildysmbol auf der **Datum und Uhrzeit ändern** Schaltfläche signalisiert, dass der Prozess ein Token für vollständigen Administratorzugriff erfordert und eine UAC-Eingabeaufforderung für erhöhte Rechte angezeigt.

**Sichern der Eingabeaufforderung für erhöhte Rechte**

Die Höherstufung wird weiter durch Weiterleiten der Aufforderung zum sicheren Desktop gesichert. Die zustimmungsaufforderungen und administratoranmeldeaufforderungen werden standardmäßig in Windows Server 2012 auf dem sicheren Desktop angezeigt. Nur Windows-Prozesse können auf den sicheren Desktop zugreifen. Höheres Maß an Sicherheit, empfehlen wir behalten die **Benutzerkontensteuerung: bei benutzeraufforderung zum sicheren Desktop wechseln** richtlinieneinstellung aktiviert ist.

Wenn eine ausführbare Datei erhöhte Rechte erfordert, wird der interaktive Desktop, und den Desktop des Benutzers, die Abkürzung zum sicheren Desktop wechselt. Der sichere Desktop Blendet den Benutzerdesktop ab und zeigt eine Eingabeaufforderung für erhöhte Rechte, die vor dem Fortfahren auf reagiert werden muss. Wenn der Benutzer klickt auf "Ja" oder nicht, der Desktop wechselt zurück zum Benutzerdesktop.

Schadsoftware kann eine Imitation des sicheren Desktops jedoch dann, wenn das Benutzerkonto steuern: Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren im Administratorbestätigungsmodus-Einstellung auf Aufforderung zur Zustimmung festgelegt ist, wird die Schadsoftware zu für erhöhte Rechte nicht erhalten, der Benutzer klickt auf Ja zu klicken. Wenn die richtlinieneinstellung auf Aufforderung zur Eingabe von Anmeldeinformationen festgelegt ist, kann Schadsoftware, die die administratoranmeldeanforderung die Anmeldeinformationen des Benutzers erfassen können. Allerdings die Schadsoftware erhält keinen Zugriff erhöhten Rechten, und das System weist andere, die Kontrolle über die Benutzeroberfläche selbst mit einem Kennwort genutzten übernehmen von Malware zu verringern.

Während der Schadsoftware eine Imitation des sicheren Desktops darstellen kann, kann nicht dieses Problem auftreten, es sei denn, ein Benutzer die Schadsoftware zuvor auf dem Computer installiert. Da Prozesse, die ein Administratorzugriffstoken erfordern unbeaufsichtigt installieren können, wenn UAC aktiviert ist, der Benutzer muss ausdrücklich seine Zustimmung erklären durch Klicken auf **Ja** oder Administratoranmeldeinformationen bereitstellt. Die spezifische Verhaltensweise der UAC-Eingabeaufforderung für erhöhte Rechte hängt von der Gruppenrichtlinie.

## <a name="uac-architecture"></a>UAC-Architektur
Im folgende Diagramm werden die UAC-Architektur.

![Diagramm mit detaillierten Informationen zu UAC-Architektur](../media/How-User-Account-Control-Works/UACArchitecture.gif)

Überprüfen Sie um jede Komponente besser zu verstehen, in der folgenden Tabelle:

|Komponente|Beschreibung|
|-------|--------|
|**Benutzer**||
|Benutzer führt eine Berechtigung|Wenn der Vorgang das Dateisystem oder die Registrierung geändert wird, wird die Virtualisierung aufgerufen. Bei allen anderen Vorgängen werden ShellExecute aufgerufen.|
|ShellExecute|ShellExecute ruft CreateProcess auf. ShellExecute sucht nach der Fehlermeldung ERROR_ELEVATION_REQUIRED von "CreateProcess". Wenn der Fehler empfangen wird, ruft ShellExecute den Anwendungsinformationen-Dienst versucht, die angeforderte Aufgabe mit der Eingabeaufforderung mit erhöhten Rechten ausführen.|
|"CreateProcess"|Wenn die Anwendung erhöhte Rechte erforderlich ist, lehnt "CreateProcess" den Aufruf mit ERROR_ELEVATION_REQUIRED ab.|
|**System**||
|Anwendungsinformationsdienst|Ein Systemdienst, mit der Startseite, die eine oder mehrere erhöhten oder Benutzerrechte, beispielsweise lokale Verwaltungsaufgaben ausführen erfordern und Anwendungen, die höhere Integritätsebenen erfordern. Anwendungsinformationen hilft dem Starten des Diensts, die Zustimmung solche Anwendungen durch ein neuer Prozess für die Anwendung mit dem vollständigen Zugriffstoken ein Administrator erstellen, wenn erhöhte Rechte erforderlich sind und (abhängig von der Gruppenrichtlinie) wird durch den Benutzer dazu angegeben.|
|Erhöhen einer ActiveX-Installation|Wenn ActiveX nicht installiert ist, überprüft das System die UAC-schiebereglerstufe. Wenn ActiveX installiert ist, die **Benutzerkontensteuerung: bei benutzeraufforderung zum sicheren Desktop wechseln** Einstellung der Gruppenrichtlinie aktiviert ist.|
|Überprüfen Sie die UAC-schiebereglerstufe|UAC verfügt jetzt über vier auswählbare Benachrichtigungsstufen und einen Schieberegler mit die Benachrichtigungsstufe ausgewählt:<br /><br /><ul><li>Hoch<br /><br />    Wenn der Schieberegler auf **immer benachrichtigen**, das System überprüft, ob der sichere Desktop aktiviert ist.</li><li>Mittel<br /><br />    Wenn der Schieberegler auf **Standard-benachrichtigen mich nur, wenn Programme versuchen, Änderungen an meinem Computer vornehmen**, die **User Account Control: nur ausführbare Dateien heraufstufen, die signiert und überprüft sind** richtlinieneinstellung aktiviert ist:<br /><br /><ul><li>Wenn die richtlinieneinstellung aktiviert ist, wird die public Key-Infrastruktur (PKI)-zertifizierungspfadüberprüfung für eine angegebene ausführbare Datei erzwungen, bevor es ausgeführt werden darf.</li><li>Wenn die richtlinieneinstellung nicht aktiviert ist (Standard), die PKI-zertifizierungspfadüberprüfung nicht erzwungen, bevor eine angegebene ausführbare Datei ausgeführt werden darf. Die **Benutzerkontensteuerung: bei benutzeraufforderung zum sicheren Desktop wechseln** Einstellung der Gruppenrichtlinie aktiviert ist.</li></ul></li><li>Niedrig<br /><br />    Wenn der Schieberegler auf **nur, wenn Programme versuchen, Änderungen an meinem Computer vornehmen benachrichtigen (Desktop nicht Abblenden)**, wird "CreateProcess" aufgerufen.</li><li>Nie benachrichtigen<br /><br />    Wenn der Schieberegler auf **nie benachrichtigen, wenn**, UAC wird nie benachrichtigen, wenn ein Programm installieren oder auf dem Computer ändern möchten. **Wichtig:** dieser Einstellung wird nicht empfohlen. Diese Einstellung ist identisch mit dem Festlegen der **Benutzerkontensteuerung: Verhalten der Eingabeaufforderung für erhöhte Rechte für Administratoren im Administratorbestätigungsmodus** richtlinieneinstellung **erhöhte Rechte ohne eingabeanforderung**.</li></ul>|
|Sichere Desktop aktiviert|Die **Benutzerkontensteuerung: bei benutzeraufforderung zum sicheren Desktop wechseln** richtlinieneinstellung aktiviert ist:<br /><br />– Wenn der sichere Desktop aktiviert ist, gehen alle Anforderungen für erhöhte Rechte auf dem sicheren Desktop unabhängig von den Einstellungen für das Verhalten der Eingabeaufforderung für Administratoren und Standardbenutzer.<br />– Wenn der sichere Desktop nicht aktiviert ist, rufen alle Anforderungen für erhöhte Rechte auf dem interaktiven Desktop des Benutzers, und die benutzerspezifischen Einstellungen für Administratoren und Standardbenutzer verwendet werden.|
|"CreateProcess"|"CreateProcess" ruft AppCompat "," Fusion "und" Installer Erkennung, um zu bewerten, ob die Anwendung erhöhte Rechte erforderlich sind. Die ausführbare Datei wird dann überprüft, um die angeforderte Ausführungsebene zu bestimmen, die im Anwendungsmanifest der ausführbaren Datei gespeichert ist. CreateProcess schlägt fehl, wenn die im Manifest angegebene angeforderte Ausführungsebene nicht das Zugriffstoken entspricht und einen Fehler (ERROR_ELEVATION_REQUIRED) an ShellExecute zurückgegeben. |
|AppCompat|Die AppCompat-Datenbank speichert Informationen in den Anwendungskompatibilitätspatch-Einträgen für eine Anwendung.|
|Fusion|Die Fusion-Datenbank speichert Informationen aus dem Anwendungsmanifesten, die die Anwendungen beschreiben. Das Manifestschema wird aktualisiert, um ein neues Level angeforderte Ausführungsebene-Feld hinzufügen.|
|Installer-Erkennung|Die installationserkennung erkennt Setup ausführbare Dateien, welche wird verhindert, dass Installationen ohne das Wissen und Zustimmung des Benutzers ausgeführt werden.|
|**Kernel**||
|Virtualisierung|Virtualisierungstechnologie wird sichergestellt, dass nicht kompatible Anwendungen nicht im Hintergrund fehlschlagen ausgeführt wird oder fehlschlägt, so, dass die Ursache nicht ermittelt werden kann. UAC bietet zudem eine Datei-und Registrierungsvirtualisierung und Protokollierung für Anwendungen, die in geschützte Bereiche schreiben.|
|Dateisystem und Registrierung|Die pro Benutzer Datei- und Registrierungsvirtualisierung leitet computerbasierte Registrierung und Datei Schreibanforderungen an entsprechenden benutzerbasierten Speicherorte. Leseanforderungen an den virtualisierten einzelbenutzerort umgeleitet werden zuerst verwendet und an den Speicherort pro Computer.|

Es ist eine Änderung in Windows Server 2012 UAC aus vorherigen Windows-Versionen. Die neue Schieberegler wird nie UAC vollständig deaktivieren. Die neue Einstellung wird:

-   Halten Sie die UAC-Dienst ausgeführt wird.

-   Ursache alle für erhöhte Rechte anfordern von Administratoren, die automatisch genehmigt werden, ohne dass eine UAC-Eingabeaufforderung initiiert.

-   Alle Anforderungen für erhöhte Rechte für Standardbenutzer automatisch ablehnen.

> [!IMPORTANT]
> Zum vollständigen Deaktivieren von UAC müssen Sie die Richtlinie deaktivieren **Benutzerkontensteuerung: alle Administratoren im Administratorbestätigungsmodus ausführen**.

> [!WARNING]
> Maßgeschneiderte Apps funktionieren nicht unter Windows Server 2012, wenn die UAC deaktiviert ist.

### <a name="virtualization"></a>Virtualisierung
Da Systemadministratoren in unternehmensumgebungen Systeme sichern versucht, viele Line-of-Business (LOB) Anwendungen sollen nur ein Standardbenutzer-Zugriffstoken zu verwenden. Daher müssen IT-Administratoren nicht den Großteil der Anwendungen zu ersetzen, wenn Windows Server 2012 mit aktivierter UAC ausgeführt.

 Windows Server 2012 enthält die Datei und registrierungsvirtualisierungstechnologie für Anwendungen, die nicht UAC-kompatibel sind und erfordern ein Administratorzugriffstoken ordnungsgemäß ausgeführt. Virtualisierung wird sichergestellt, dass auch Anwendungen, die nicht UAC-kompatible sind mit Windows Server 2012 kompatibel sind. Bei einer administrativen, die nicht UAC-kompatibel ist, in einem geschützten Verzeichnis, z. B. Programme, schreiben, liefert die UAC der Anwendung eine eigene virtualisierte Ansicht der Ressource, die sie versucht zu ändern. Die virtualisierte Kopie wird im Profil des Benutzers verwaltet. Mit dieser Strategie erstellt eine separate Kopie der virtualisierten Datei für jeden Benutzer, der die nicht kompatible Anwendung ausgeführt wird.

Die meisten Anwendungsaufgaben werden ordnungsgemäß mithilfe von Virtualisierungsfeatures. Obwohl die Virtualisierung der meisten Anwendungen ausführen können, ist es, einen kurzfristigen Patch und nicht für eine langfristige Lösung. Anwendungsentwickler sollten ihre Anwendungen kompatibel mit dem Windows Server 2012-Logo-Programm so bald wie möglich, anstatt sich auf die Datei, Ordner-und Registrierungsvirtualisierung verlassen zu ändern.

Virtualisierung ist keine Option in den folgenden Szenarien:

1.  Virtualisierung gilt nicht für Anwendungen, die erhöhte Rechte und mit einem Token für vollen Administratorzugriff ausgeführt werden.

2.  Virtualisierung unterstützt nur 32-Bit-Anwendungen. Die 64-Bit-Anwendungen ohne erhöhte Rechte erhalten einfach Zugriff verweigert wird, wenn sie versuchen, einen Handle (einen eindeutigen Bezeichner) für ein Windows-Objekt abzurufen. Systemeigene Windows 64-Bit-Apps müssen mit UAC kompatibel sein und Schreiben von Daten in den richtigen Ort.

3.  Virtualisierung ist für eine Anwendung deaktiviert, wenn die Anwendung ein Anwendungsmanifest mit einem angeforderten ausführungsstufenattribut enthält.

### <a name="request-execution-levels"></a>Anforderungsausführungsstufen
Ein Anwendungsmanifest ist eine XML-Datei, die beschreibt und identifiziert die freigegebenen und privaten Side-by-Side Assemblys, die eine Anwendung, zur Laufzeit gebunden werden soll. In Windows Server 2012 enthält das Anwendungsmanifest Einträge für Kompatibilitätszwecke für UAC-Anwendung. Administrative Anwendungen, die einen Eintrag im Anwendungsmanifest enthalten fordert den Benutzer für die Berechtigung zum Zugriffstoken des Benutzers zugreifen. Auch wenn sie einen Eintrag im App-Manifest verfügen, können die meisten administratoranwendungen ohne Änderung mithilfe von Anwendungskompatibilitätspatches ausführen. Anwendungskompatibilitätspatches handelt es sich um Datenbankeinträge, die Anwendungen zu, die nicht UAC-kompatible ermöglichen ordnungsgemäß mit Windows Server 2012 sind.

Alle UAC-kompatible Anwendungen sollten eine angeforderte Ausführungsebene zum Anwendungsmanifest hinzugefügt haben. Wenn die Anwendung Administratorzugriff auf das System erfordert, wird sichergestellt dann die Anwendung mit einer angeforderten Ausführungsstufe von "Administrator erforderlich" kennzeichnen, dass das System dieses Programm als eine administrative App identifiziert und die erforderlichen rechteerweiterungsschritte ausführt. Die angeforderten Ausführungsebenen geben die Berechtigungen für eine Anwendung erforderlichen an.

### <a name="installer-detection-technology"></a>Technologie für Installationserkennung
Installationsprogramme sind Anwendungen, die zum Bereitstellen von Software. Die meisten Installationsprogramme schreiben Daten in Systemverzeichnisse und Registrierungsschlüssel. Diese geschützten Systemspeicherorte sind in der Regel beschreibbaren nur von einem Administrator in der Technologie für installationserkennung, was bedeutet, dass Standardbenutzer keinen ausreichenden Zugriff auf Programme zu installieren. Windows Server 2012 ermittelt ganzheitlich Installationsprogramme und fordert Administratoranmeldeinformationen oder Genehmigung vom Administratorbenutzer, um die Ausführung mit Zugriffsrechten. Windows Server 2012 ermittelt zudem ganzheitlich Updates und Programme, mit die Anwendungen deinstalliert werden. Eines der Entwurfsziele für die Benutzerkontensteuerung soll verhindern, dass Installationen ohne das Wissen des Benutzers ausgeführt wird, und stimmen, da Installationsprogramme in geschützte Bereiche des Dateisystems und der Registrierung schreiben.

Die installationserkennung gilt für:

-   ausführbare 32-Bit-Dateien.

-   Anwendungen ohne Attribut für eine angeforderte Ausführungsebene.

-   Interaktive Prozesse, die als Standardbenutzer mit aktivierter UAC ausgeführt werden.

Bevor ein 32-Bit-Prozess erstellt wird, werden die folgenden Attribute überprüft, um festzustellen, ob es sich um ein Installationsprogramm ist:

-   Der Dateiname enthält Schlüsselwörter wie "install" "setup", oder "Update".

-   Felder für versionsverwaltungsressourcen enthalten die folgenden Schlüsselwörter: Anbieter, Firmenname, Produktname, DateiBeschreibung, Ursprünglicher Dateiname, interner Name und exportname.

-   Schlüsselwörter im Side-by-Side-Manifest werden in die ausführbare Datei eingebettet.

-   Schlüsselwörter in spezifischen "STRINGTABLE"-Einträgen werden in der ausführbaren Datei verknüpft.

-   Wichtige Attribute in den ressourcenskriptdaten werden in der ausführbaren Datei verknüpft.

-   Es gibt zielbytesequenzen in der ausführbaren Datei.

> [!NOTE]
> Gemeinsame Merkmale aufweisen, die in verschiedenen installationstechnologien beobachtet wurden die Schlüsselwörter und Bytesequenzen abgeleitet.

> [!NOTE]
> Die Benutzerkontensteuerung: Anwendungsinstallationen erkennen und Eingabeaufforderung für erhöhte für die Erkennung von Installationsprogrammen damit Installationsprogramme erkannt aktiviert werden muss. Diese Einstellung kann ist standardmäßig aktiviert und lokal mithilfe von konfiguriert das Snap-in "Lokale Sicherheitsrichtlinie" (Secpol.msc) oder für die Domäne, Organisationseinheit oder bestimmte Gruppen von der Gruppenrichtlinie (Gpedit.msc) konfiguriert werden.


