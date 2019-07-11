---
title: Überlegungen zum Arbeitsspeicher-Nutzung in AD DS zur leistungsoptimierung
description: Die speicherauslastung durch den Prozess "Lsass.exe" auf Domänencontrollern, auf denen Windows Server 2012 R2, 2016 und 2019 ausgeführt werden.
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; lindakup
author: Teresa-Motiv
ms.date: 7/3/2019
ms.openlocfilehash: dd33124d7d480f3670fa2781f567eaaa28abbce6
ms.sourcegitcommit: be243a92f09048ca80f85d71555ea6ee3751d712
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67799782"
---
# <a name="memory-usage-considerations-for-ad-ds-performance-tuning"></a>Überlegungen zum Arbeitsspeicher-Nutzung, zur leistungsoptimierung für AD DS

Dieser Artikel beschreibt einige Grundlagen der Local Security Authority Subsystem Service (LSASS, auch bekannt als der Prozess Lsass.exe), bewährte Methoden für die Konfiguration für LSASS und Erwartungen für die arbeitsspeicherauslastung. In diesem Artikel soll als Leitfaden bei der Analyse der LSASS-Leistung und speicherauslastung verwenden auf einem Domänencontroller (DCs) verwendet werden. Die Informationen in diesem Artikel ist möglicherweise nützlich, wenn Sie Fragen zum Optimieren und Konfigurieren von Servern und Domänencontrollern zum Optimieren dieses Moduls verfügen.  

LSASS ist verantwortlich für die Verwaltung der lokalen Sicherheitsautorität (LSA) Domäne Sicherheitsauthentifizierung und Verwaltung von Active Directory. LSASS übernimmt die Authentifizierung für sowohl der Client als auch der Server, und er steuert auch die Active Directory-Modul. LSASS ist verantwortlich für die folgenden Komponenten:  

- Lokale Sicherheitsautorität
- Der NetLogon-Dienst
- Sicherheitsdienst für die Sicherheitskontenverwaltung (SAM)
- LSA-Server-Dienst
- Secure Sockets Layer (SSL)
- Kerberos v5 authentication protocol
- NTLM-Authentifizierungsprotokoll
- Andere Authentifizierungspaketen, die in die lokale Sicherheitsautorität geladen werden.

Der Active Directory-Datenbank-Dienste (NTDSAI.dll) arbeiten Sie mit der Extensible Storage Engine (ESE, ESENT.dll).

Hier ist ein visuelles Datenbankdiagramm LSASS der Auslastung des Speichers auf einem Domänencontroller aus:

![Diagramm der Komponenten, die speichernutzung durch LSASS](media/domain-controller-lsass-memory-usage.png)  

Die Größe des Arbeitsspeichers, den LSASS auf einem Domänencontroller verwendet, die in Übereinstimmung mit der Verwendung von Active Directory wird erhöht. Wenn Daten abgefragt werden, wird es im Arbeitsspeicher zwischengespeichert. Daher ist es normal, LSASS, die mit der Größe des Arbeitsspeichers, der größer als die Größe der Datei der Active Directory-Datenbank (NTDS.dit) angezeigt.

Wie im Diagramm dargestellt, kann LSASS-speicherauslastung in mehreren Teilen, einschließlich der Puffercache von ESE-Datenbank, die ESE-Versionsspeicher und andere unterteilt werden. Im weiteren Verlauf dieses Artikels bietet einen Einblick in jedem dieser Teile.

## <a name="ese-database-buffer-cache"></a>Cache für die Puffer von ESE-Datenbank  
Der größten Variablen arbeitsspeicherauslastung LSASS wird der Puffercache von ESE-Datenbank. Die Größe des Caches reichen von weniger als 1 MB auf die Größe der gesamten Datenbank. Da ein größerer Cache die Leistung verbessert wird, versucht die Datenbank-Engine für die Active Directory (ESENT) ab, den Cache so groß wie möglich zu halten. Die Größe des Caches mit ungenügendem Arbeitsspeicher auf dem Computer unterschiedlich ist, ist die maximale Größe des ESE-Datenbank Puffercache *nur* durch den physischen RAM-Kapazität auf dem Computer beschränkt. Solange es keine andere Arbeitsspeicher wird kann der Cache auf die Größe der Active Directory-NTDS.dit-Datenbankdatei anwachsen. Je mehr von der Datenbank, die zwischengespeichert werden kann, desto besser die Leistung des Domänencontrollers werden.  
  
> [!NOTE]
> Aufgrund der Art und Weise, dass die Datenbank mit dem Algorithmus funktioniert, auf einem 64-Bit-System, auf dem die Datenbank kleiner als der verfügbare Arbeitsspeicher ist, ist, die Zwischenspeicherung Cache für die Datenbank größer als die Größe der Datenbank von 30 bis 40 Prozent vergrößert werden kann.

## <a name="ese-version-store"></a>Das ESE-Versionsspeicher

Es gibt Variable speicherauslastung durch den ESE-Versionsspeicher (der rote Teil in der Abbildung oben). Die Menge an Arbeitsspeicher, die verwendet wird, hängt davon ab, gibt an, ob Sie über Windows Server-2019 oder ältere Versionen von Windows verfügen.

- In Windows Server-Versionen, die Windows Server-2019 Jahrhunderten standardmäßig verwendeten LSASS bis zu ca. 400 MB Arbeitsspeicher (abhängig von der Anzahl der CPUs) auf einem 64-Bit-Computer für die ESE-Version kann zu speichern. Weitere Informationen zur Verwendung von der Versionsspeicher finden Sie unter den folgenden ASKDS Blogbeitrag von Ryan Ries: [Die Store-Version aufgerufen wird und sie sind alle aus Buckets](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/The-Version-Store-Called-and-They-8217-re-All-Out-of-Buckets/ba-p/400415).

- In Windows Server-2019 Darstellung ist natürlich vereinfacht, und beim Dienst selbst NTDS erste gestartet wird, wird die Store-Größe des ESE-Version jetzt als 10 % des physischen Arbeitsspeichers mit einer Länge von 400MB und maximal 4GB berechnet. Gute Informationen zu diesem und Version Store zur Problembehandlung finden Sie in einem anderen hervorragenden Blog von Ryan Ries: [Vertiefung: Active Directory ESE Version Store Änderungen im Server-2019](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/Deep-Dive-Active-Directory-ESE-Version-Store-Changes-in-Server/ba-p/400510).

## <a name="other-memory-use"></a>Andere arbeitsspeichernutzung

Abschließend ist Code, Stapel, Heaps und verschiedene Datenstrukturen fester Größe (z. B. dem Schemacache). Die Größe des Arbeitsspeichers, den LSASS verwendet variieren je nach Auslastung auf dem Computer. Wenn die Anzahl der ausgeführten Threads zunimmt, steigt die Anzahl der Speicherstapel. LSASS werden durchschnittlich 100 MB bis 300 MB an Arbeitsspeicher für die festen Komponenten verwendet. Wenn eine größere Menge an RAM installiert ist, können LSASS mehr Arbeitsspeicher und weniger virtuellen Speicher verwenden.

**Beschränken Sie, minimieren Sie die Anzahl der Programme auf Ihrem Domänencontroller, oder fügen Sie weitere RAM hinzu, falls zutreffend**

Für eine optimale Leistung wird LSASS so viel Arbeitsspeicher wie möglich auf einem bestimmten DC. LSASS aufgibt, um Arbeitsspeicher als andere Prozesse danach zu Fragen. Die Idee ist, Optimieren der Leistung von LSASS, während Sie weiterhin einkalkulieren anderer Prozesse, die auf einem Computer ausgeführt werden können. Die Liste der Programme in Betracht ziehen, enthält die überwachungs-Agents. Einige Kunden verfügen über separate Agents für verschiedene Serverfunktionen, die viele RAM-Ressourcen nutzen können. Einige können viele WMI-Abfragen ausgeben, die für die wir ein paar Details unten haben.

Aus diesem Grund und die Leistung zu erhöhen ist es sich bewährt, begrenzen oder die Anzahl der Programme auf einem DC zu minimieren. Wenn keine Anforderungen mehr Arbeitsspeicher sind, verwendet LSASS dieser Arbeitsspeicher zum Zwischenspeichern von Active Directory-Datenbank, und daher eine optimale Leistung zu erzielen.

Wenn Sie feststellen, dass ein DC Leistungsprobleme aufweist, auch für Prozesse mit erheblichen arbeitsspeicherauslastung ansehen. Diese haben möglicherweise ein Problem, die Sie beheben müssen. Sie können Microsoft-Komponenten enthalten. Stellen Sie sicher, dass Sie mit Schritt halten aktuelle Wartungsupdates&mdash;Microsoft bietet Lösungen für eine zu hohe speicherauslastung als Teil der qualitätsupdates, die auch die Leistung Ihres DC möglicherweise.

Es gibt integrierte OS-Funktionen, die erhebliche RAM abhängig vom Profil Nutzung nutzen können:

- **Dateiserver**. DCs sind auch Dateiserver für SYSVOL- und Netlogon-Freigaben, die Wartung von Gruppenrichtlinien und Skripts für die Richtlinie und Start/Anmeldeskripts.
  Allerdings sehen wir Kunden, die Domänencontroller verwenden, um anderen Inhalt zu bedienen. SMB-Dateiservers würde dann RAM, zum Nachverfolgen von aktiven Clients nutzen, aber es vor allem des Inhalts der Datei würde des Betriebssystem-Datei-Caches zu wachsen und mit den Datenbankcache der ESE Arbeitsspeicher konkurrieren.  

- **WMI-Abfragen**. Überwachungslösungen stellen häufig viele WMI-Abfragen. Eine einzelne Abfrage möglicherweise schnell ausführen. Häufig ist es die Anzahl der Aufrufe, bei der ein gewisser Overhead – auftreten, insbesondere dann, wenn der überwachungslösung in Azure Stack neue Ereignisse aus verschiedenen Ereignisprotokollen extrahieren, die Windows verwaltet.  

  Das Ereignisprotokoll, das von dem meisten Volume erstellt, ist in der Regel das Sicherheitsereignisprotokoll. Und dies ist auch im Ereignisprotokoll, das Administratoren für die Sicherheit an, vor allem von Domänencontrollern gesammelt werden sollen.  

  Der WMI-Dienst verwendet eine dynamische Speicherbelegungsschema, die Abfragen optimiert. Aus diesem Grund werden die WMI-Dienst möglicherweise viel Arbeitsspeicher belegen, konkurrierende erneut mit dem Cache des ESE-Datenbank zugewiesen.  
