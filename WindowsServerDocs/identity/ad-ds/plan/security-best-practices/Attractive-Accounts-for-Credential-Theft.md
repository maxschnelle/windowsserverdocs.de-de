---
ms.assetid: 34244b53-1206-4f5b-8c4d-3ebf574d8e24
title: Attraktive Konten für den Diebstahl von Anmeldeinformationen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8e5d2b01f73127f84f700dab3518b66687f0294f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863101"
---
# <a name="attractive-accounts-for-credential-theft"></a>Attraktive Konten für den Diebstahl von Anmeldeinformationen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Angriffen mit gestohlenen Anmeldeinformationen sind in dem ein Angreifer die höchste geringen (Stamm, Administrator oder SYSTEM je nach Betriebssystem verwendet) anfänglich erhält Zugriff auf einen Computer in einem Netzwerk, und klicken Sie dann verwendet, die kostenlos verfügbare Tools nutzen, um Anmeldeinformationen zu extrahieren. von der Sitzungen, die von anderen angemeldeten Konten. Je nach Systemkonfiguration können diese Anmeldeinformationen in Form von Hashes, Tickets oder auch Klartext-Kennwörtern extrahiert werden. Wenn eines der genutzten Anmeldeinformationen für lokale Konten, die wahrscheinlich auf anderen Computern im Netzwerk (z. B. Administratorkonten in Windows oder Root-Konten in OS x, UNIX oder Linux) vorhanden sind, zeigt der Angreifer die Anmeldeinformationen auf anderen Computern für das Netzwerk Gefährdung auf weiteren Computern zu verbreiten und versuchen Sie es zum Abrufen der Anmeldeinformationen von zwei bestimmte Arten von Konten:  

1.  Privilegierter Domänenkonten mit breit angelegte und tief Berechtigungen (d.h., Konten, die über Administratorrechte, auf mehreren Computern und in Active Directory verfügen). Diese Konten möglicherweise nicht Mitglied einer der höchsten Berechtigungen Gruppen in Active Directory, aber sie können über die entsprechende auf Administratorebene-Berechtigungen auf verschiedenen Servern oder Arbeitsstationen in die Domäne oder Gesamtstruktur, wodurch sie effektiv so leistungsfähig wie Mitglieder von privilegierten Gruppen in Active Directory. In den meisten Fällen sind Konten, die über umfassende Adressbereiche von der Windows-Infrastruktur hohe Berechtigungen gewährt wurden Dienstkonten, also die Dienstkonten für Breite und Tiefe der Berechtigung immer bewertet werden soll.  

2.  "Sehr wichtig Person" Domänenkonten (VIP). Im Kontext dieses Dokuments ist ein VIP-Konto auf, jedes Konto, das Zugriff auf Informationen, die ein Angreifer (geistiges Eigentum und andere vertrauliche Informationen) möchte, oder ein beliebiges Konto, mit denen der Angreifer Zugriff auf diese Informationen werden können. Beispiele für diese Benutzerkonten sind:  

    1.  Führungskräfte, deren Konten Zugriff auf sensible Unternehmensdaten haben  

    2.  Konten für die Helpdesk-Mitarbeiter, die für die Verwaltung der Computer und Anwendungen ein, die Führungskräfte zuständig sind  

    3.  Konten für rechtliche Mitarbeiter, die Zugriff auf Dokumente von der Organisation Gebot und den Vertrag, besitzen die Dokumente für die eigene Organisation oder die clientorganisationen sind  

    4.  Produktplaner mit Zugriff auf Pläne und Spezifikationen für Produkte in der Entwicklung für eine Unternehmens-pipeline, unabhängig von den Arten von Produkten, die das Unternehmen macht.  

    5.  Forscher, deren Konten verwendet werden, auf der Studie, ein Produkt Formeln oder eine beliebige andere Recherche für einen Angreifer von Interesse sind  

Da sehr privilegierte Konten in Active Directory verwendet werden können, Gefährdung weitergegeben werden und zum Bearbeiten von VIP-Konten oder die Daten, die sie zugreifen können, sind die nützlichsten Konten für Angriffen mit gestohlenen Anmeldeinformationen Konten, die Mitglieder der Organisations-Admins sind, Domänen-Admins und Administratoren Gruppen in Active Directory.  

Da Domänencontroller die Repositorys für AD DS-Datenbank sind und Domänencontroller vollen Zugriff auf alle Daten in Active Directory haben, sind Domänencontroller auch für die Gefährdung, ob parallel mit Angriffen mit gestohlenen Anmeldeinformationen, oder als Ziel verwendet eine oder mehrere sehr privilegierte Active Directory-Konten sind beschädigt worden. Obwohl zahlreiche Publikationen (und viele Angreifer) auf die Gruppenmitgliedschaften der Domänen-Admins zu, beim Beschreiben von Angriffen mit gestohlenen Anmeldeinformationen von Pass-the-Hash und anderen konzentrieren (beschriebene [die Active Directory-Angriffsfläche verkleinern](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)) , ein Konto, das ein Mitglied einer der hier aufgeführten Gruppen ist kann verwendet werden, um die gesamte AD DS-Installation zu gefährden.  

> [!NOTE]  
> Umfassende Informationen zu Pass-the-Hash und anderen Angriffen mit gestohlenen Anmeldeinformationen zu erhalten, finden Sie unter den [Mitigating Pass-the-Hash (PTH)-Angriffe und anderen Techniken zum Diebstahl von Anmeldeinformationen](https://download.microsoft.com/download/7/7/A/77ABC5BD-8320-41AF-863C-6ECFB10CB4B9/Mitigating%20Pass-the-Hash%20(PtH)%20Attacks%20and%20Other%20Credential%20Theft%20Techniques_English.pdf) aufgeführt, die im Whitepaper [Anhang M : Links zu Dokumenten und empfohlene Lektüre](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md). Weitere Informationen über Angriffe durch entschlossene die werden manchmal als "Fortgeschrittene dauerhafte Bedrohungen" (APTs), finden Sie unter [Angreifer bestimmt und Ziel von Angriffen](https://www.microsoft.com/download/details.aspx?id=34793).  

## <a name="activities-that-increase-the-likelihood-of-compromise"></a>Aktivitäten, die die Wahrscheinlichkeit einer Gefährdung erhöhen  
Da das Ziel der Diebstahl von Anmeldeinformationen in der Regel hoch privilegierter Domänenkonten und VIP-Konten ist, ist es wichtig, dass Administratoren sich der Aktivitäten, die die Wahrscheinlichkeit des Erfolgs eines Angriffs Diebstahl von Anmeldeinformationen zu erhöhen. Obwohl Angreifer auch VIP-Konten, abzielen, wenn hohe Berechtigungen auf Systemen oder in der Domäne nicht in virtuellen IP-Adressen angegeben sind, erfordert Diebstahl von Anmeldeinformationen für ihre anderen Arten von Angriffen, z. B. Social engineering der VIP um geheime Informationen bereitzustellen. Oder der Angreifer muss zuerst rufen Sie privilegierten Zugriff auf ein System, auf welche VIP Anmeldeinformationen zwischengespeichert werden. Aus diesem Grund werden Aktivitäten, die die erhöhen die Wahrscheinlichkeit, dass die hier beschriebenen Diebstahl von Anmeldeinformationen Schwerpunkt die Übernahme von sehr privilegierten administrativen Anmeldeinformationen zu verhindern. Diese Aktivitäten sind allgemeine Mechanismen, die mit denen Angreifer Systeme zum Abrufen von privilegierter Anmeldeinformationen beeinträchtigen können.  

### <a name="logging-on-to-unsecured-computers-with-privileged-accounts"></a>Anmelden an der ungeschützten Computer mit privilegierten Konten  
Die Core-Schwachstelle, die Angriffen mit gestohlenen Anmeldeinformationen erfolgreich ausgeführt werden kann ist die Anmeldung bei Computern, die nicht mit Konten, die Allgemein sicher und in der gesamten Umgebung stark privilegierten. Diese Anmeldungen können das Ergebnis der verschiedenen Fehlkonfigurationen, die hier beschriebenen sein.  

#### <a name="not-maintaining-separate-administrative-credentials"></a>Verwalten Sie keine Separate Administrative Anmeldeinformationen  
Obwohl dies relativ selten, bei der Bewertung der verschiedenen AD DS-Installationen ist, haben wir IT-Mitarbeiter, die über ein einziges Konto für alle ihre Arbeit gefunden. Das Konto ist ein Mitglied mindestens einer der meisten sehr privilegierten Gruppen in Active Directory und ist das gleiche Konto, mit denen die Mitarbeiter melden Sie sich auf ihren Arbeitsstationen am Morgen, überprüfen Sie ihre e-Mails, Websites und Herunterladen von Inhalt an ihre Computer. Wenn Benutzer mit Konten ausführen zu können, die lokale Administratorrechte und Berechtigungen gewährt werden, weisen sie den lokalen Computer zum Abschließen der Gefährdung. Wenn diese Konten auch Mitglieder der Gruppen mit hohen Berechtigungen in Active Directory sind, weisen sie die ganze Gesamtstruktur gefährden, somit ganz einfach für einen Angreifer, vollständige Kontrolle über die Active Directory und Windows-Umgebung zu erhalten.  

Auf ähnliche Weise haben in einigen Umgebungen herausgestellt, dass die gleichen Benutzernamen und Kennwörter für Stamm-Konten auf nicht-Windows-Computern verwendet werden, da in der Windows-Umgebung verwendet werden, wodurch Angreifer Gefährdung von UNIX- oder Linux-Systemen mit Windows-Systemen zu erweitern. und umgekehrt.

#### <a name="logons-to-compromised-workstations-or-member-servers-with-privileged-accounts"></a>Anmeldungen gefährdeten Arbeitsstationen oder die Mitgliedsserver mit privilegierten Konten  
Wenn ein Domänenkonto mit weit reichenden Berechtigungen zur interaktiven Anmeldung zu einer gefährdeten Arbeitsstation oder die Mitgliedsserver verwendet wird, kann dieser kompromittierten Computer-Anmeldeinformationen für ein Konto erhalten Sie, die das System anmeldet.  

#### <a name="unsecured-administrative-workstations"></a>Unsichere administrativen Arbeitsstationen  
In vielen Organisationen werden von IT-Mitarbeiter mehrere Konten verwendet. Ein Konto für die Anmeldung des Mitarbeiters-Arbeitsstation dient, und da diese IT-Mitarbeiter sind, sie häufig haben lokale Administratorrechte auf ihren Arbeitsstationen. In einigen Fällen UAC ist aktiviert, sodass der Benutzer mit mindestens eine geteilten Zugriff erhält links token bei der Anmeldung und müssen erhöhen, wenn Administratorrechte erforderlich sind. Wenn diese Benutzer Wartungsaktivitäten durchführen, sie in der Regel lokal installierten Verwaltungstools verwenden und geben Sie die Anmeldeinformationen für ihre Domäne privilegierte Konten durch Auswählen der **als Administrator ausführen** Option oder die Anmeldeinformationen bei Aufforderung. Obwohl diese Konfiguration entsprechenden mag, stellt es die Umgebung, da zu gefährden:  

-   Der "regular" an, das der Mitarbeiter verwendet wird, zum Anmelden an ihrer Arbeitsstation verfügt über lokale Administratorrechte, der Computer ist anfällig für [Drive-By-](https://www.microsoft.com/security/sir/glossary/drive-by-download-sites.aspx) Angriffe, die in dem der Benutzer davon überzeugt ist Malware installieren.  

-   Die Malware, die im Kontext eines Administratorkontos installiert ist, der Computer kann jetzt verwendet werden, um erfassen Tastatureingaben, den Inhalt der Zwischenablage, Screenshots und Arbeitsspeicher-Anmeldeinformationen, die alle, die eine Offenlegung von Anmeldeinformationen für eine leistungsstarke Domäne führen kann das Konto.  

Die Probleme in diesem Szenario gibt es zwei Gründe. Zunächst jedoch separate Konten für lokale und Domänenprinzipale Verwaltung verwendet werden, der Computer nicht geschützt ist und nicht die Konten vor Diebstahl geschützt. Zweitens wurden die normale Benutzerkonto und das Administratorkonto zu viele Rechte und Berechtigungen erteilt.  

### <a name="browsing-the-internet-with-a-highly-privileged-account"></a>Browsen im Internet mit einem Konto mit weit reichenden Berechtigungen  
Benutzer melden Sie sich bei Computern mit Konten, die Mitglieder der lokalen Administratorgruppe auf dem Computer oder der privilegierten Gruppen in Active Directory sind, und navigieren, die Sie dann im Internet (oder einem gefährdeten Intranet) verfügbar machen, den lokalen Computer und die Verzeichnis, zu manipulieren.  

Zugriff auf ein böswilliger Website mit einem Browser mit Administratorprivilegien ausgeführt, können Angreifer, schädlichen Code auf dem lokalen Computer im Rahmen der privilegierten Benutzer hinterlegen. Wenn der Benutzer über lokale Administratorrechte auf dem Computer verfügt, können Angreifer täuschen und den Benutzer herunterladen von Schadsoftware oder öffnen die e-Mail-Anlagen, die Sicherheitslücken von Anwendungen zu nutzen, und nutzen die Berechtigungen des Benutzers zum Extrahieren, lokal zwischengespeichert Anmeldeinformationen für alle aktiven Benutzer auf dem Computer. Wenn der Benutzer im Verzeichnis durch die Mitgliedschaft in der Organisations-Admins, Domänen-Admins oder Administratorgruppen in Active Directory über Administratorrechte verfügt, kann der Angreifer Anmeldeinformationen für die Domäne zu extrahieren und verwenden, um die gesamten AD DS-Domäne oder Gesamtstruktur beeinträchtigen, ohne Sie zu einem beliebigen anderen Computer in der Gesamtstruktur beeinträchtigen.  

### <a name="configuring-local-privileged-accounts-with-the-same-credentials-across-systems"></a>Konfigurieren von lokalen privilegierten Konten mit den gleichen Anmeldeinformationen über Systeme hinweg  
Konfigurieren den gleichen lokalen Administratorkontonamen und das Kennwort auf viele oder alle Computer ermöglicht Anmeldeinformationen gestohlen werden, von der SAM-Datenbank auf einem Computer verwendet werden, um alle anderen Computer zu erlangen, die die gleichen Anmeldeinformationen verwenden. Zumindest sollten Sie verschiedene Kennwörter für lokale Administratorkonten für jede Domäne eingebundenes System verwenden. Konten für lokale Administratoren können auch eindeutig benannt, aber verschiedene Kennwörter für privilegierte lokalen des Systems-Konten mit ist ausreichend, um sicherzustellen, dass die Anmeldeinformationen auf anderen Systemen verwendet werden können.  

### <a name="overpopulation-and-overuse-of-privileged-domain-groups"></a>Overpopulation oder übermäßiger Verwendung privilegierter Gruppen  
Erteilen die Mitgliedschaft in den Enterprise Agreement, DA oder BA Gruppen in einer Domäne erstellt ein Ziel für Angreifer dar. Je größer die Anzahl der Mitglieder dieser Gruppen, desto größer die Wahrscheinlichkeit, dass ein privilegierter Benutzer möglicherweise unbeabsichtigt Missbrauch von Anmeldeinformationen und verfügbar machen, um Diebstahl von Anmeldeinformationen-Angriffe. Stellt einen Mechanismus bereit, die mit dem die privilegierten Anmeldeinformationen unter Umständen stellen und verwendet werden, die AD DS-Domäne und Gesamtstruktur gefährden möglichen, jede Arbeitsstation oder einem Server, der ein privilegierter Benutzer sich anmeldet.  

### <a name="poorly-secured-domain-controllers"></a>Nahezu Ungesicherten Domänencontroller  
Domänencontroller enthalten eine Kopie der AD DS-Datenbank von einer Domäne. Im Fall von Read-only-Domänencontroller enthält das lokale Replikat der Datenbank die Anmeldeinformationen für nur eine Teilmenge der Konten im Verzeichnis privilegierter Domänenkonten standardmäßig werden. Auf Domänencontrollern mit Lese-/ Schreibzugriff verwaltet jeder Domänencontroller für ein vollständiges Replikat der AD DS-Datenbank, einschließlich der Anmeldeinformationen nicht nur für berechtigte Benutzer wie Domänen-Admins, aber die privilegierte Konten wie DC-Konten oder der Domäne Krbtgt Konto an, das das Konto, das dem der KDC-Dienst auf einem Domänencontroller zugeordnet ist. Wenn Anwendungen, die nicht für die Domäne-Controller-Funktionen erforderlich sind, die auf Domänencontrollern installiert werden oder ob der Domänencontroller nicht repräsentative Motoröltemperatur gepatcht und gesichert werden, können Angreifer diese über ungepatchte Sicherheitsrisiken, oder sie kompromittieren kann andere Angriffsvektoren zum Installieren von bösartigen Software direkt auf diese nutzen.  

## <a name="privilege-elevation-and-propagation"></a>Erhöhung der Rechte und Weitergabe  
Unabhängig von der Angriffsmethoden verwendet Active Directory richtet sich immer, wenn eine Windows-Umgebung angegriffen wird, da es sich letztlich um den Zugriff steuert, was die Angreifer werden sollen. Dies bedeutet nicht, dass das gesamte Verzeichnis, jedoch angewendet werden. Bestimmte Konten, Server und Komponenten der Infrastruktur sind in der Regel das primäre Ziel von Angriffen mit Active Directory. Diese Konten werden wie folgt beschrieben werden.  

### <a name="permanent-privileged-accounts"></a>Dauerhaften privilegierten Konten  
Da es sich bei der Einführung von Active Directory wird es möglich, Benutzerkonten zum Erstellen von Active Directory-Gesamtstruktur verwenden, die über weitreichende Privilegien und klicken Sie dann Delegaten Rechte und Berechtigungen, die zum Ausführen der täglichen Verwaltung weniger privilegierten Konten erforderlich wurde. Mitgliedschaft in der Organisations-Admins, Domänen-Admins oder Administratoren Gruppen in Active Directory muss nur vorübergehend und nur selten in einer Umgebung, die mit minimalprivilegien Ansätze für die tägliche Verwaltung implementiert.  

Dauerhafte privilegierte Konten sind Konten, die in privilegierten Gruppen platziert und bleibt es von Tag zu Tag wurden. Wenn Ihre Organisation fünf Konten in der Gruppe "Domänen-Admins" für eine Domäne platziert, möglich die fünf Konten gezielte 24-Stunden einen Tag, sieben Tage die Woche. Allerdings ist die tatsächlichen Bedarfs zum Verwenden von Konten mit Domänen-Admins-Berechtigungen in der Regel nur für bestimmte domänenweite-Konfiguration, und klicken Sie für kurze Zeit.  

### <a name="vip-accounts"></a>VIP-Konten  
Eine häufig übersehene Ziel in Active Directory-sicherheitsverletzungen ist die Konten von "sehr wichtig Persons" (oder virtuellen IP-Adressen) in einer Organisation. Privilegierte Konten werden als Ziel verwendet werden, da diese Konten Zugriff, für Angreifer, die es ihnen gefährden oder sogar zerstört Zielsystemen, ermöglicht erteilen können, wie weiter oben in diesem Abschnitt beschrieben.  

### <a name="privilege-attached-active-directory-accounts"></a>"Berechtigung Attached" Active Directory-Konten  
"Berechtigung attached" Active Directory-Konten als Domänenkonten, die nicht Mitglied einer der Gruppen, die das höchste Maß an Berechtigungen in Active Directory vorgenommen wurden, aber stattdessen hohe Berechtigungen auf viele Server erteilt worden und Arbeitsstationen in der Umgebung. Diese Konten sind die meisten häufig domänenbasierter Konten, die zum Ausführen der Dienste auf der Domäne verbundenen Systemen, in der Regel für Anwendungen auf große Teile der Infrastruktur konfiguriert sind. Obwohl diese Konten keine Berechtigungen in Active Directory verfügen, wenn sie hohe Berechtigungen auf großen Anzahl von Systemen erteilt werden, sie dienen zum gefährden oder auch zerstören große Segmente der Infrastruktur, erreichen denselben Effekt wie die Gefährdung einer privilegierten Active Directory-Konto.  
