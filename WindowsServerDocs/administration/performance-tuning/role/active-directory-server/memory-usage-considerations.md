---
title: Überlegungen zur Speicherauslastung bei der AD DS Leistungsoptimierung
description: Speicherauslastung durch den LSASS. exe-Prozess auf Domänen Controllern, auf denen Windows Server 2012 R2, 2016 und 2019 ausgeführt wird.
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: v-tea; lindakup
author: Teresa-Motiv
ms.date: 7/3/2019
ms.openlocfilehash: 55ac47d835874ddb8e160603f08cbafa985aad2a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370288"
---
# <a name="memory-usage-considerations-for-ad-ds-performance-tuning"></a>Überlegungen zur Speicherauslastung für die AD DS Leistungsoptimierung

In diesem Artikel werden einige Grundlagen des Subsystemdienst für die lokale Sicherheitsautorität (LSASS, auch bekannt als Lsass. exe-Prozess), bewährte Methoden für die Konfiguration von LSASS und die Erwartungen an die Speicherauslastung beschrieben. Dieser Artikel sollte als Leitfaden bei der Analyse der LSASS-Leistung und der Arbeitsspeicher Verwendung auf Domänen Controllern (DCS) verwendet werden. Die Informationen in diesem Artikel können nützlich sein, wenn Sie Fragen zum Optimieren und Konfigurieren von Servern und DCS haben, um diese Engine zu optimieren.  

LSASS ist für die Verwaltung der lokalen Sicherheits Autorität (Local Security Authority, LSA) und der Active Directory Verwaltung verantwortlich. LSASS übernimmt die Authentifizierung sowohl für den Client als auch für den Server und steuert auch das Active Directory Modul. LSASS ist für die folgenden Komponenten verantwortlich:  

- Lokale Sicherheitsautorität
- Anmeldedienst
- Security Accounts Manager (Sam)-Dienst
- LSA-Server Dienst
- Secure Sockets Layer (SSL)
- Kerberos V5-Authentifizierungsprotokoll
- NTLM-Authentifizierungsprotokoll
- Andere Authentifizierungs Pakete, die in LSA geladen werden

Die Active Directory-Datenbankdienste (ntdsai. dll) funktionieren mit dem Extensible Storage Engine (ESE, ESENT. dll).

Im folgenden finden Sie ein visuelles Diagramm der LSASS-Speicherauslastung auf einem DC:

![Diagramm der Komponenten, die LSASS-Speicher verwenden](media/domain-controller-lsass-memory-usage.png)  

Die Menge an Arbeitsspeicher, die LSASS auf einem Domänen Controller verwendet, erhöht sich entsprechend der Active Directory Nutzung. Wenn die Daten abgefragt werden, werden Sie im Arbeitsspeicher zwischengespeichert. Daher ist es normal, dass LSASS eine Menge an Arbeitsspeicher verwendet, die größer ist als die Größe der Active Directory Datenbankdatei (NTDS. dit).

Wie im Diagramm dargestellt, kann die LSASS-Speicherauslastung in mehrere Teile aufgeteilt werden, darunter der ESE-Daten Bank Puffer Cache, der ESE-Versionsspeicher und andere. Im restlichen Teil dieses Artikels erhalten Sie einen Einblick in die einzelnen Komponenten.

## <a name="ese-database-buffer-cache"></a>ESE-Daten Bank Puffer Cache  
Die größte Variable Speicherauslastung in LSASS ist der ESE-Daten Bank Puffer Cache. Die Größe des Caches kann zwischen weniger als 1 MB und der Größe der gesamten Datenbank liegen. Da ein größerer Cache die Leistung verbessert, versucht die Datenbank-Engine für Active Directory (ESENT), den Cache so groß wie möglich zu halten. Während die Größe des Caches mit der Arbeitsspeicher Auslastung des Computers variiert, wird die maximale Größe des Puffer Caches der ESE-Datenbank *nur* durch den physischen RAM beschränkt, der auf dem Computer installiert ist. Solange keine andere Arbeitsspeicher Auslastung vorhanden ist, kann der Cache auf die Größe der Active Directory NTDS. dit-Datenbankdatei anwachsen. Umso mehr der Datenbank, die zwischengespeichert werden kann, desto besser ist die Leistung des DC.  
  
> [!NOTE]
> Aufgrund der Art und Weise, wie der Algorithmus für die Daten Bank Zwischenspeicherung funktioniert, kann der Daten Bank Cache auf einem 64-Bit-System, auf dem die Datenbankgröße kleiner ist als der verfügbare Arbeitsspeicher, größer als die Datenbankgröße um 30 bis 40 Prozent zunehmen.

## <a name="ese-version-store"></a>ESE-Versionsspeicher

Es gibt eine Variable Speicherauslastung durch den ESE-Versionsspeicher (den roten Teil im obigen Diagramm). Die Menge des verwendeten Arbeitsspeichers hängt davon ab, ob Sie über Windows Server 2019 oder ältere Versionen von Windows verfügen.

- In Windows Server-Versionen, die mit Windows Server 2019 vorlaufen, kann LSASS standardmäßig bis zu 400 MB Arbeitsspeicher (abhängig von der Anzahl der CPUs) auf einem 64-Bit-Computer für den ESE-Versionsspeicher verwenden. Weitere Informationen zur Verwendung des Versionsspeicher finden Sie im folgenden askds-Blogbeitrag von Ryan Ries: [dem Versionsspeicher mit dem Namen, und Sie sind nicht in der](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/The-Version-Store-Called-and-They-8217-re-All-Out-of-Buckets/ba-p/400415)bucketdatei.

- In Windows Server 2019 wird dies vereinfacht. wenn der NTDS-Dienst zum ersten Mal gestartet wird, wird die ESE-Versionsspeicher Größe nun als 10% des physischen Arbeitsspeichers berechnet, mit einem Minimum von 400 MB und einem Maximum von 4 GB. Ausführliche Informationen zu dieser und zur Problembehandlung für den Versionsspeicher finden Sie in einem anderen tollen Blog von Ryan Ries: [Deep Dive: Active Directory ESE-Versionsspeicher Änderungen in Server 2019](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/Deep-Dive-Active-Directory-ESE-Version-Store-Changes-in-Server/ba-p/400510).

## <a name="other-memory-use"></a>Weitere Arbeitsspeicher Nutzung

Schließlich gibt es Code, Stapel, Heaps und verschiedene Datenstrukturen fester Größe (z. b. den Schema Cache). Die Menge an Arbeitsspeicher, die LSASS verwendet, kann je nach Auslastung des Computers variieren. Wenn die Anzahl der laufenden Threads zunimmt, wird auch die Anzahl der Speicher Stapel verwendet. Im Durchschnitt verwendet LSASS für diese festgelegten Komponenten 100 MB bis 300 MB Arbeitsspeicher. Wenn eine größere RAM-Menge installiert ist, kann LSASS mehr RAM und weniger virtuellen Arbeitsspeicher verwenden.

**Beschränken oder minimieren Sie die Anzahl der Programme auf Ihrem Domänen Controller, oder fügen Sie ggf. zusätzlichen RAM hinzu**

Um eine optimale Leistung zu erzielen, benötigt LSASS so viel Arbeitsspeicher wie möglich auf einem bestimmten Domänen Controller. LSASS gibt diesen RAM aus, wie er von anderen Prozessen angefordert wird. Die Idee besteht darin, die Leistung von LSASS zu optimieren, während gleichzeitig andere Prozesse berücksichtigt werden, die möglicherweise auf einem Computer ausgeführt werden. Die Liste der zu überwachenden Programme umfasst das Überwachen von Agents. Einige Kunden haben separate Agents für verschiedene Serverfunktionen, die beträchtliche RAM-Ressourcen verbrauchen können. Einige können viele WMI-Abfragen ausgeben, für die wir unten einige Details finden.

Aus diesem Grund empfiehlt es sich, die Anzahl der Programme auf einem DC einzuschränken oder zu minimieren, um die Leistung zu verbessern. Wenn keine Speicheranforderungen vorhanden sind, verwendet LSASS diesen Arbeitsspeicher, um die Active Directory Datenbank zwischenzuspeichern und somit eine optimale Leistung zu erzielen.

Wenn Sie bemerken, dass ein Domänen Controller Leistungsprobleme aufweist, achten Sie auch auf Prozesse mit erheblicher Speicherauslastung. Dies kann ein Problem sein, das Sie bei der Problembehandlung benötigen. Sie können Microsoft-Komponenten enthalten. Stellen Sie sicher, dass Sie mit den neuesten Wartungsupdates Schritt halten&mdash;Microsoft enthält Lösungen für eine übermäßige Speicherauslastung im Rahmen der Qualitäts Updates, die möglicherweise auch die Leistung Ihres Domänen Controllers unterstützen.

Es gibt integrierte Betriebssystem Einrichtungen, die je nach Nutzungsprofil erheblichen RAM beanspruchen können:

- **Dateiserver**. DCS sind auch Dateiserver für SYSVOL-und NETLOGON-Freigaben, die Gruppenrichtlinien und Skripts für Richtlinien-und Start-/Anmeldeskripts.
  Wir sehen jedoch, dass Kunden DCS zum Dienst anderer Dateiinhalte verwenden. Der SMB-Dateiserver beansprucht dann Arbeitsspeicher, um die aktiven Clients zu überprüfen. der Dateiinhalt würde jedoch dazu führen, dass der Betriebssystem-Dateicache wächst und mit dem ESE-Daten Bank Cache für RAM konkurriert.  

- **WMI-Abfragen**. Überwachungslösungen führen häufig zu vielen WMI-Abfragen. Die Ausführung einer einzelnen Abfrage ist möglicherweise kostengünstig. Häufig handelt es sich um die Anzahl der Aufrufe, die einen gewissen Aufwand verursachen, insbesondere, wenn die Überwachungslösungen neue Ereignisse aus den verschiedenen Ereignisprotokollen extrahieren, die von Windows verwaltet werden.  

  Das Ereignisprotokoll, das das größte Volume erzeugt, ist in der Regel das Sicherheits Ereignisprotokoll. Dies ist auch das Ereignisprotokoll, das Sicherheits Administratoren erfassen möchten, insbesondere von DCS.  

  Der WMI-Dienst verwendet ein dynamisches Speicher Belegungs Schema, das Abfragen optimiert. Daher kann der WMI-Dienst viel Arbeitsspeicher zuweisen, der wiederum mit dem ESE-Daten Bank Cache konkurriert.  
