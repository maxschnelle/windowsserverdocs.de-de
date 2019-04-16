---
ms.assetid: 34244b53-1206-4f5b-8c4d-3ebf574d8e24
title: "Attraktive Konten für den Diebstahl von Anmeldeinformationen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ae1bfe017e8b21c3abfcdc137153b0fd379053fa
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="attractive-accounts-for-credential-theft"></a>Attraktive Konten für den Diebstahl von Anmeldeinformationen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Methoden des anmeldeinformationsdiebstahls sind in dem ein Angreifer die höchsten-Berechtigung (Root, Administrator oder SYSTEM, je nach Betriebssystem verwendet) zunächst erhält Zugriff auf einen Computer in einem Netzwerk, und klicken Sie dann verwendet, die kostenlos verfügbare Tools zum Extrahieren von Anmeldeinformationen aus der Sitzungen von anderen Konten angemeldet. Abhängig von der Systemkonfiguration können diese Anmeldeinformationen in Form von Hashes, Tickets und sogar Klartextkennwörter extrahiert werden. Wenn eine der genutzten Anmeldeinformationen für lokale Konten, die wahrscheinlich auf anderen Computern im Netzwerk (z. B. Administratorkonten in Windows oder Root-Konten in OS x, UNIX- oder Linux) vorhanden sind, zeigt der Angreifer die Anmeldeinformationen auf anderen Computern im Netzwerk Gefährdung auf weiteren Computern zu verteilen und zu versuchen, die Anmeldeinformationen des zwei bestimmte Arten von Konten zu erhalten. :  

1.  Privilegierter Domänenkonten mit umfassenden und Tiefen Berechtigungen (d. h., Konten, die über Administratorrechte auf vielen Computern und in Active Directory verfügen). Diese Konten möglicherweise nicht Mitglied einer der höchsten Rechte Gruppen in Active Directory, aber sie können über die Berechtigung Administratorebene-Berechtigungen auf verschiedenen Servern oder Arbeitsstationen in der Domäne oder Gesamtstruktur, wodurch sie effektiv so leistungsfähig wie Mitgliedern privilegierter Gruppen in Active Directory. In den meisten Fällen sind Konten, die hohe Rechte über umfassende Adressbereiche von der Windows-Infrastruktur verfügen Dienstkonten, damit Dienstkonten immer Tiefe und der Rechte bewertet werden soll.  

2.  "Sehr wichtig Person" Domänenkonten (VIP). Im Kontext dieses Dokuments ist eine VIP-Konto ein Konto, das Zugriff auf Informationen, die ein Angreifer (geistigen Eigentums und andere vertrauliche Informationen) möchte oder jedes Konto, das Erteilen der Angreifer Zugriff auf diese Informationen verwendet werden kann. Beispiele für diese Benutzerkonten:  

    1.  Führungskräfte, deren Konten Zugriff auf sensible Unternehmensdaten haben  

    2.  Konten für den Helpdesk-Mitarbeiter, die für die Verwaltung der Computer und Anwendungen, die von Führungskräften verwendet zuständig sind  

    3.  Konten für die gesetzliche Mitarbeiter mit Zugriff auf Ihre Auktionen verfolgen und Vertrag Dokumente eines Unternehmens, ob die Dokumente für ihre eigenen Organisation oder Client Organisationen sind  

    4.  Pläne und Spezifikationen für Produkte in der Entwicklung des Unternehmens zugreifen Produktplaner pipeline, unabhängig davon, welche Produkte, die das Unternehmen gibt  

    5.  Entwicklern, deren Konten verwendet werden, den Zugriff auf Studie Daten, Formeln Produkt oder eine beliebige andere Recherche für einen Angreifer von Interesse  

Da privilegierte Konten in Active Directory verwendet werden können, Gefährdung weitergegeben und Bearbeiten von VIP-Konten oder die Daten, die sie zugreifen können, sind die nützlichsten Konten für die Methoden des anmeldeinformationsdiebstahls Konten, die Mitglieder der Gruppen Organisations-Admins, Domänen-Admins und Administratoren in Active Directory sind.  

Da Domänencontroller den-Repositorys für die AD DS-Datenbank sind und Domänencontroller vollen Zugriff auf alle Daten in Active Directory haben, sind Domänencontroller auch für eine Gefährdung vorliegt, als Ziel verwendet, ob parallel mit Methoden des anmeldeinformationsdiebstahls oder nach einem oder mehreren sehr privilegierten Active Directory Konten gefährdet sind. Obwohl zahlreiche Publikationen (und viele Angreifer) auf die Domänen-Admins-Gruppenmitgliedschaften konzentrieren, wenn Sie Pass-the-Hash und anderen Methoden des anmeldeinformationsdiebstahls beschreiben (beschriebenen [der Active Directory-Angriffsfläche](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)), ein Konto, das Mitglied der Gruppen, die hier aufgeführten ist kann verwendet werden, um die gesamte AD DS-Installation zu gefährden.  

> [!NOTE]  
> Umfassende Informationen zu Pass-the-Hash und anderen Methoden des anmeldeinformationsdiebstahls, finden Sie unter der [Mitigating Pass-the-Hash (PTH)-Angriffen und anderen Techniken zum Diebstahl](https://download.microsoft.com/download/7/7/A/77ABC5BD-8320-41AF-863C-6ECFB10CB4B9/Mitigating%20Pass-the-Hash%20(PtH)%20Attacks%20and%20Other%20Credential%20Theft%20Techniques_English.pdf) aufgeführt, die im Whitepaper [Anhang M: Dokumentenlinks und empfohlene lesen](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md). Weitere Informationen über Angriffe durch entschlossene die werden manchmal als "Fortgeschrittene dauerhafte Bedrohungen" (APTs), finden Sie unter [Angreifer bestimmt und Ziel-Angriffe](https://www.microsoft.com/download/details.aspx?id=34793).  

## <a name="activities-that-increase-the-likelihood-of-compromise"></a>Aktivitäten, die erhöhen die Wahrscheinlichkeit, dass der Gefährdung  
Da das Ziel des Diebstahls von Anmeldeinformationen in der Regel um Domänenkonten sehr privilegierten und VIP-Konten ist, ist es wichtig, Administratoren Standardfeature Aktivitäten, die die Wahrscheinlichkeit des Erfolgs eines Angriffs Diebstahl von Anmeldeinformationen zu erhöhen. Obwohl auch VIP-Konten Angreifer VIPs hohe Rechte auf Systemen oder in der Domäne nicht angegeben sind, erfordert Diebstahl von Anmeldeinformationen andere Arten von Angriffen, z. B. Social engineering-der VIP um geheime Informationen bereitzustellen. Oder der Angreifer muss zunächst privilegierten Zugriff auf ein System, auf welche VIP Anmeldeinformationen zwischengespeichert werden. Aus diesem Grund sind Aktivitäten, die die Wahrscheinlichkeit des Diebstahls von Anmeldeinformationen hier beschriebenen erhöhen konzentriert sich in erster Linie verhindert die Übernahme von sehr privilegierten administrativen Anmeldeinformationen. Diese Aktivitäten sind allgemeine Mechanismen, die mit denen Angreifer Systeme privilegierte Anmeldeinformationen erhalten beeinträchtigen können.  

### <a name="logging-on-to-unsecured-computers-with-privileged-accounts"></a>Unsichere von Computern mit privilegierten Konten anmelden  
Die Core-Schwachstelle, die Methoden des anmeldeinformationsdiebstahls erfolgreich ermöglicht ist das Anmelden bei Computern, die nicht mit Konten, die Allgemein sicher und tief privilegierten in der gesamten Umgebung. Diese Anmeldung kann das Ergebnis der verschiedenen Fehlkonfigurationen, die hier beschriebenen sein.  

#### <a name="not-maintaining-separate-administrative-credentials"></a>Keinen verwaltet Separate Administrative Anmeldeinformationen  
Obwohl dies bei der Bewertung der verschiedenen AD DS-Installationen relativ selten ist, haben wir die IT-Mitarbeiter ein einzelnes Konto für alle ihre Arbeit mit festgestellt. Das Konto ist Mitglied mindestens eines der am häufigsten sehr privilegierten Gruppen in Active Directory und wird dasselbe Konto, dass die Mitarbeiter verwenden auf ihren Arbeitsstationen am Morgen anmelden per e-Mail überprüfen, Websites im Internet durchsuchen und Herunterladen von Inhalt an ihren Computern. Beim Ausführen von Benutzern mit Konten, die lokale Administratorrechte und Berechtigungen gewährt werden sie den lokalen Computer zum Abschließen der Gefährdung verfügbar machen. Wenn diese Konten auch Mitglieder der am häufigsten privilegierten Gruppen in Active Directory sind, verfügbar machen sie die Gesamtstruktur zu einer Gefährdung erleichtern im Grunde ein Angreifer die vollständige Kontrolle über die Active Directory und Windows-Umgebung zu erhalten.  

In manchen Umgebungen, haben wir auf ähnliche Weise festgestellt, dass die gleichen Benutzernamen und Kennwörter für die Stamm-Konten auf nicht-Windows-Computern verwendet werden, wie in der Windows-Umgebung verwendet werden, wodurch Angreifer Gefährdung von UNIX- oder Linux-Systemen mit Windows-Systemen und umgekehrt zu erweitern.

#### <a name="logons-to-compromised-workstations-or-member-servers-with-privileged-accounts"></a>Anmeldungen gefährdeten Arbeitsstationen oder Mitgliedsservern mit privilegierten Konten  
Wenn ein privilegierter Domänenkonto verwendet wird, zu einer gefährdeten Arbeitsstation oder einem Mitgliedsserver interaktiv anmelden, kann die betroffenen Computer-Anmeldeinformationen für ein Konto nutzen, die das System anmeldet.  

#### <a name="unsecured-administrative-workstations"></a>Unsichere administrativen Arbeitsstationen  
In vielen Organisationen verwenden IT-Mitarbeiter mehrere Konten. Ein Konto für die Anmeldung des Mitarbeiters Arbeitsstation verwendet wird, und da diese IT-Mitarbeiter sind, sie häufig lokale Administratorrechte auf ihren Arbeitsstationen. In einigen Fällen UAC ist aktiviert, sodass der Benutzer mindestens eine geteilte Zugriff erhält links token bei der Anmeldung und müssen erhöhen, wenn Administratorrechte erforderlich sind. Wenn diese Benutzer Verwaltungsaufgaben ausführen, sie in der Regel lokal installierte Managementtools verwenden, und geben Sie die Anmeldeinformationen für ihre Domäne privilegierten Konten durch Auswahl der **als Administrator ausführen** option oder erhalten Sie die Anmeldeinformationen, wenn Sie aufgefordert werden. Obwohl diese Konfiguration geeigneten mag, macht es die Umgebung, da zu gefährden:  

-   "Regular" Benutzerkontos ein, das der Mitarbeiter wird verwendet, um auf ihre Arbeitsstation anmelden über lokale Administratorrechte, die Computer sind anfällig für [Laufwerk herunterladen](https://www.microsoft.com/security/sir/glossary/drive-by-download-sites.aspx) Angriffe, die in dem der Benutzer davon überzeugt ist Malware installieren.  

-   Die Schadsoftware wird im Kontext eines Administratorkontos installiert ist, der Computer kann jetzt verwendet werden, zum Erfassen von Tastaturanschlägen, Zwischenablage, Screenshots und Arbeitsspeicher-Anmeldeinformationen, die Gefährdung der Anmeldeinformationen eines Domänenkontos leistungsstarke führen kann.  

Die Probleme in diesem Szenario sind zwei. Zunächst jedoch separate Konten für die Verwaltung von lokalen und verwendet werden, der Computer nicht geschützt ist und nicht die Konten vor Diebstahl geschützt. Zweitens wurde das Standardbenutzerkonto und das Administratorkonto übermäßige Rechte und Berechtigungen erteilt.  

### <a name="browsing-the-internet-with-a-highly-privileged-account"></a>Browsen im Internet mit einem sehr privilegierten Konto  
Benutzer melden Sie sich am Computer mit Konten, die Mitglieder der lokalen Administratorgruppe auf dem Computer oder Mitgliedern privilegierter Gruppen in Active Directory und mit wem und Durchsuchen Sie das Internet (oder einem gefährdeten Intranet) verfügbar machen, dem lokalen Computer und das Verzeichnis zu gefährden.  

Zugriff auf eine in böswilliger Absicht erstellten Website in einem Browser mit Administratorrechten kann ein schädlichen Code auf dem lokalen Computer im Kontext des privilegierten Benutzers einzahlen Angreifer. Wenn der Benutzer über lokale Administratorrechte auf dem Computer verfügt, Angreifer möglicherweise täuschen und des Benutzers schädlichen Code herunterladen, oder öffnen die e-Mail-Anlagen, die Sicherheitslücken nutzen und nutzen die Berechtigungen des Benutzers lokal extrahieren zwischengespeicherten Anmeldeinformationen für alle aktiven Benutzer auf dem Computer. Wenn der Benutzer im Verzeichnis durch die Mitgliedschaft in der Organisations-Admins, Domänen-Admins oder Administratorgruppen in Active Directory über Administratorrechte verfügt, kann der Angreifer extrahieren Sie die Anmeldeinformationen und verwenden, um die gesamte AD DS-Domäne oder Gesamtstruktur gefährden, ohne alle anderen Computer in der Gesamtstruktur beeinträchtigen.  

### <a name="configuring-local-privileged-accounts-with-the-same-credentials-across-systems"></a>Konfigurieren von lokalen privilegierte Konten mit denselben Anmeldeinformationen über Systeme  
Konfigurieren den gleichen lokalen Administratorkontonamen und das Kennwort auf alle Computer ermöglicht Anmeldeinformationen gestohlen aus der SAM-Datenbank auf einem Computer verwendet werden, um alle anderen Computer zu gefährden, die die gleichen Anmeldeinformationen verwenden. Zumindest sollten Sie verschiedene Kennwörter für lokale Administratorkonten für jede Domäne System verwenden. Lokaler Administratorkonten können auch eindeutig benannt, aber verwenden verschiedene Kennwörter für jedes System privilegierten lokale Konten ist ausreichend, um sicherzustellen, dass die Anmeldeinformationen auf anderen Systemen verwendet werden können.  

### <a name="overpopulation-and-overuse-of-privileged-domain-groups"></a>Overpopulation und die übermäßige Verwendung privilegierter Gruppen  
Erteilen die Mitgliedschaft in Gruppen EA, DA oder BA in einer Domäne erstellt ein Ziel für Angreifer. Je größer die Anzahl von Mitgliedern dieser Gruppen, desto größer die Wahrscheinlichkeit, dass ein privilegierter Benutzer möglicherweise versehentlich, die Anmeldeinformationen missbrauchen und verfügbar machen, um den Diebstahl von Anmeldeinformationen von Angriffen. Jede Arbeitsstation oder einem Server für die Anmeldung eines Benutzers privilegierten Domäne zeigt einen möglichen Mechanismus, mit dem die privilegierten Anmeldeinformationen des Benutzers geerntet und der AD DS-Domäne und der Gesamtstruktur beeinträchtigen.  

### <a name="poorly-secured-domain-controllers"></a>Schlecht gesicherten Domänencontrollern  
Domänencontroller untergebracht ein Replikat der AD DS-Datenbank von einer Domäne. Im Fall von schreibgeschützten Domänencontrollern enthält die lokale Kopie der Datenbank die Anmeldeinformationen für nur eine Teilmenge der Konten in das Verzeichnis, die der privilegierter Domänenkonten in der Standardeinstellung sind. Auf Domänencontrollern mit Lese-/ Schreibzugriff jeder Domänencontroller verwaltet ein vollständiges Replikat der AD DS-Datenbank, einschließlich der Anmeldeinformationen nicht nur für berechtigte Benutzer z. B. Domänen-Admins, aber auf Domänencontrollern-service-privilegierte Konten wie Domänencontrollerkonten oder der Domäne Krbtgt-Konto, das das Konto, das KDC zugeordnet wird. Wenn zusätzliche Anwendungen, die nicht für die Funktionalität eines Domänencontrollers erforderlich sind auf Domänencontrollern installiert werden, wenn Domänencontroller nicht repräsentative Motoröltemperatur sind Patches und gesichert sind, ein Angreifer können sie über Sicherheitsrisiken beeinträchtigen oder nutzen sie anderen Angriffsmethoden, um direkt auf schädliche Software zu installieren.  

## <a name="privilege-elevation-and-propagation"></a>Erhöhte Rechte und Weitergabe  
Unabhängig von der Angriffsmethoden verwendet Active Directory zielt immer, wenn eine Windows-Umgebung angegriffen wird, Zugriff letztendlich bestimmt, was die Angreifer möchten. Dies bedeutet nicht, dass das gesamte Verzeichnis, jedoch ausgerichtet ist. Bestimmte Konten, Server und Infrastrukturkomponenten sind in der Regel die primären Ziele von Angriffen auf Active Directory. Diese Konten werden wie folgt beschrieben.  

### <a name="permanent-privileged-accounts"></a>Permanente privilegierte Konten  
Da der Einführung von Active Directory wird es möglich, Benutzerkonten verwenden, die sehr privilegierten Active Directory-Gesamtstruktur zu erstellen, und klicken Sie dann Delegaten Rechte und erforderliche Berechtigungen zum Ausführen der täglichen Verwaltung weniger privilegierten Konten wurde. Mitgliedschaft in der Gruppe Organisations-Admins, Domänen-Admins oder Administratoren in Active Directory muss nur vorübergehend und selten in einer Umgebung, die geringsten Ansätze für die tägliche Verwaltung implementiert.  

Permanente privilegierte Konten sind Konten, die in privilegierten Gruppen angeordnet und Links es von Tag zu Tag wurden. Wenn Ihre Organisation fünf Konten in der Gruppe "Domänen-Admins" für eine Domäne platziert, möglich diese fünf Konten zielgerichtete 24-Stunden täglich, sieben Tage die Woche. Tatsächliche müssen zur Verwendung von Konten mit Domänen-Admins-Berechtigungen ist jedoch in der Regel nur für bestimmte domänenweite Konfiguration und für kurze Zeit.  

### <a name="vip-accounts"></a>VIP-Konten  
Ein häufig übersehenes Ziel in Active Directory unterrichten ist die Konten "sehr wichtig, Personen" (oder VIPs) in einer Organisation. Privilegierte Konten werden als Ziel verwendet werden, da diese Konten Zugriff, für Angreifer, die Möglichkeit gewähren können Systemverwaltungssoftware auch Zielsysteme, wie weiter oben in diesem Abschnitt beschrieben.  

### <a name="privilege-attached-active-directory-accounts"></a>"Rechte angefügten" Active Directory-Konten  
"Rechte angefügten" Active Directory-Konten sind Domänenkonten, die nicht Mitglied einer der Gruppen, die die höchsten Rechte in Active Directory vorgenommen wurden, aber stattdessen hohe Rechte auf zahlreichen Servern und Arbeitsstationen in der Umgebung gewährt wurden. Diese Konten sind die meisten häufig domänenbasierten Konten, die zum Ausführen der Dienste auf einer Domäne Angehörige Systeme in der Regel für Anwendungsbeispiele für große Teile der Infrastruktur konfiguriert sind. Obwohl diese Konten keine Rechte in Active Directory verfügen, wenn sie hohe Rechte auf großen Anzahl von Systemen gewährt werden, können sie Systemverwaltungssoftware auch große Segmente der Infrastruktur, erreichen dieselbe Wirkung wie die Gefährdung von einem privilegierten Active Directory-Konto verwendet werden.  
