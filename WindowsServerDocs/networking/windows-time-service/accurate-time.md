---
ms.assetid: 72a90d00-56ee-48a9-9fae-64cbad29556c
title: Genaue Zeit für Windows Server 2016
description: Die Genauigkeit der Zeitsynchronisierung in Windows Server 2016 wurde erheblich verbessert, während die NTP-Kompatibilität mit älteren Windows-Versionen vollständig abwärts bleibt.
author: shortpatti
ms.author: dacuo
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 2e8e9e86f81596c85219c37c07d8fd2e95cc3a49
ms.sourcegitcommit: 10331ff4f74bac50e208ba8ec8a63d10cfa768cc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/15/2020
ms.locfileid: "75953081"
---
# <a name="accurate-time-for-windows-server-2016"></a>Genaue Zeit für Windows Server 2016

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

Der Windows-Zeit Dienst ist eine Komponente, die ein Plug-in-Modell für Client-und Serverzeit-Synchronisierungs Anbieter verwendet.  Es gibt zwei integrierte Client Anbieter unter Windows, und es sind Plug-ins von Drittanbietern verfügbar. Ein Anbieter verwendet [NTP (RFC 1305)](https://tools.ietf.org/html/rfc1305) oder [MS-NTP](https://msdn.microsoft.com/library/cc246877.aspx) , um die lokale Systemzeit mit einem NTP-und/oder MS-NTP-kompatiblen Referenz Server zu synchronisieren. Der andere Anbieter ist für Hyper-v und synchronisiert virtuelle Computer (Virtual Machines, VM) mit dem Hyper-v-Host.  Wenn mehrere Anbieter vorhanden sind, wählt Windows den besten Anbieter mithilfe von Stratum Level First, gefolgt von der Stamm Verzögerung, der Stamm-und der Zeit Abweichung.

> [!NOTE]
> Eine kurze Übersicht über den Windows-Zeitdienst bietet dieses [allgemeine Übersichtsvideo](https://aka.ms/WS2016TimeVideo).

In diesem Thema wird erläutert... Diese Themen beziehen sich auf die Aktivierung der exakten Zeit: 

- Verbesserungen
- Messungen
- Empfehlungen

> [!IMPORTANT]
> Ein Nachtrag, auf den der Artikel Windows 2016-Zeit genaue Zeit verweist, kann [hier](https://windocs.blob.core.windows.net/windocs/WindowsTimeSyncAccuracy_Addendum.pdf)heruntergeladen werden.  In diesem Dokument finden Sie weitere Informationen zu unseren Methoden zum Testen und messen.

> [!NOTE] 
> Das Windows-Zeit Anbieter-Plug-in-Modell ist [auf TechNet dokumentiert](https://msdn.microsoft.com/library/windows/desktop/ms725475%28v=vs.85%29.aspx).

## <a name="domain-hierarchy"></a>Domänen Hierarchie
Domänen-und eigenständige Konfigurationen funktionieren unterschiedlich.

- Domänen Mitglieder verwenden ein sicheres NTP-Protokoll, bei dem die-Authentifizierung verwendet wird, um die Sicherheit und Authentizität des Zeit Verweises sicherzustellen.  Domänen Mitglieder werden mit einer Masteruhr synchronisiert, die von der Domänen Hierarchie und einem Bewertungssystem bestimmt wird.  In einer Domäne gibt es eine hierarchische Schicht von Zeit-stratums, bei der jeder Domänen Controller auf einen übergeordneten DC mit einem präziseren Zeit-Stratum verweist.  Die Hierarchie wird in den PDC oder einen Domänen Controller in der Stamm Gesamtstruktur aufgelöst, oder es handelt sich um einen Domänen Controller mit dem domänenflag gtimeserv, das einen guten Zeit Server für die Domäne angibt.  Weitere Informationen finden Sie weiter unten im Abschnitt [angeben eines lokalen zuverlässigen Zeit Dienstanbieter mit gtimeserv.

- Eigenständige Computer sind so konfiguriert, dass time.Windows.com standardmäßig verwendet wird.  Dieser Name wird von Ihrem DNS-Server aufgelöst, der auf eine Ressource im Besitz von Microsoft verweisen soll.  Wie alle Remote Verweise, die sich auf Remote Verweise beziehen, kann die Synchronisierung verhindern.  Netzwerk Datenverkehr und asymmetrische Netzwerk Pfade können die Genauigkeit der Zeitsynchronisierung beeinträchtigen.  Bei einer Genauigkeit von 1 MS können Sie nicht von Remote Zeitquellen abhängen.

Da Hyper-V-Gäste über mindestens zwei Windows-Zeit Anbieter verfügen, aus denen Sie auswählen können, die hostzeit und NTP, werden bei der Ausführung als Gast möglicherweise unterschiedliche Verhaltensweisen mit einer Domäne oder eigenständig angezeigt.

> [!NOTE] 
> Weitere Informationen zur Domänen Hierarchie und zum Bewertungssystem finden Sie unter ["Was ist der Windows-Zeit Dienst?"](https://blogs.msdn.microsoft.com/w32time/2007/07/07/what-is-windows-time-service/) . .

> [!NOTE]
> Stratum ist ein Konzept, das sowohl für den NTP-als auch für den Hyper-V-Anbieter verwendet wird, und sein Wert gibt den Standort in der Hierarchie an.  Stratum 1 ist für die Uhr der höchsten Ebene reserviert, und Stratum 0 ist für die Hardware reserviert, die als korrekt angesehen wird und nur wenig oder gar keine Verzögerung zugeordnet ist.  Stratum 2 spricht mit Stratum 1-Servern, Stratum 3 bis Stratum 2 usw.  Obwohl ein niedrigerer strator häufig eine genauere Uhr angibt, ist es möglich, Abweichungen zu finden.  W32Time akzeptiert auch Zeit von Stratum 15 oder niedriger.  Um den Stratum eines Clients anzuzeigen, verwenden Sie *W32tm/Query "aus/Status*.

## <a name="critical-factors-for-accurate-time"></a>Wichtige Faktoren für die genaue Zeit
In jedem Fall gibt es für eine genaue Zeit drei wichtige Faktoren:

1. **Solid Source Clock** : die quelluhr in Ihrer Domäne muss stabil und genau sein. Dies bedeutet in der Regel, dass ein GPS-Gerät installiert oder auf eine Stratum 1-Quelle verwiesen wird, wobei #3 berücksichtigt wird. Wenn Sie über zwei Boote auf dem Wasser verfügen und versuchen, die Höhe von eins im Vergleich zum anderen zu messen, ist die Genauigkeit am besten, wenn das quellboot sehr stabil ist und sich nicht bewegt. Das gleiche gilt für die Zeit, und wenn Ihre quelluhr nicht stabil ist, wird die gesamte Kette der synchronisierten Uhren in jeder Phase beeinflusst und vergrößert. Außerdem muss darauf zugegriffen werden können, weil die Zeitsynchronisierung durch Unterbrechungen der Verbindung beeinträchtigt wird. Und schließlich muss es sicher sein. Wenn der Zeit Verweis nicht ordnungsgemäß verwaltet wird oder von einer potenziell böswilligen Partei betrieben wird, können Sie Ihre Domäne für zeitbasierte Angriffe verfügbar machen.
2. **Stabile Clientuhr** : eine stabile Client Uhren gewährleistet, dass die natürliche Abweichung des Oszillators containerbar ist.  NTP verwendet mehrere Stichproben von potenziell mehreren NTP-Servern, um die lokale Computer-Uhr zu bedinieren und zu übernehmen.  Sie führt nicht zu einem Schritt der Zeit Änderungen, sondern verlangsamt oder beschleunigt die lokale Uhr, sodass Sie die genaue Zeit schnell erreichen und zwischen den NTP-Anforderungen genau bleiben.  Wenn der Oszillator der Client Computeruhr jedoch nicht stabil ist, können mehr Schwankungen zwischen den Anpassungen auftreten, und die Algorithmen, die von Windows verwendet werden, um die Uhr zu bedinieren, funktionieren nicht ordnungsgemäß.  In einigen Fällen können Firmwareupdates für eine genaue Zeit benötigt werden.
3. **Symmetrische NTP-Kommunikation** : Es ist wichtig, dass die Verbindung für die NTP-Kommunikation symmetrisch ist.  NTP verwendet Berechnungen, um die Zeit anzupassen, bei der der Netzwerk Patch symmetrisch ist.  Wenn der Pfad, der vom NTP-Paket an den Server weitergegeben wird, eine andere Zeitspanne benötigt, wird die Genauigkeit beeinträchtigt.  Beispielsweise kann sich der Pfad aufgrund von Änderungen in der Netzwerktopologie ändern oder durch Geräte weitergeleitet werden, die unterschiedliche Schnittstellen Geschwindigkeiten aufweisen.

Bei Akku Geräten, sowohl Mobil als auch portabel, müssen Sie verschiedene Strategien in Erwägung gezogen.  Gemäß unserer Empfehlung erfordert die Beibehaltung der exakten Zeit, dass die Uhr einmal pro Sekunde diszipliniert wird, was mit der Takt Aktualisierungshäufigkeit korreliert. Diese Einstellungen verbrauchen mehr Akkuleistung als erwartet und können den Energiesparmodus beeinträchtigen, der in Windows für solche Geräte verfügbar ist. Akku Geräte verfügen auch über bestimmte Energie Modi, die die Ausführung aller Anwendungen verhindern, was die W32time's-Fähigkeit beeinträchtigt, die Uhr zu disziplinieren und eine genaue Zeit zu gewährleisten. Außerdem sind Uhren auf mobilen Geräten möglicherweise nicht sehr genau, wenn Sie mit beginnen.  Umgebungsbedingungen wirken sich auf die Takt Genauigkeit aus, und ein mobiles Gerät kann von einer Umgebungs Bedingung zum nächsten wechseln, was die Fähigkeit beeinträchtigt, Zeit genau zu halten.  Daher wird von Microsoft nicht empfohlen, tragbare Geräte mit hoher Genauigkeit in Akku Betrieb zu setzen. 

## <a name="why-is-time-important"></a>Warum ist Zeit wichtig?  
Es gibt viele verschiedene Gründe, weshalb Sie möglicherweise eine genaue Zeit benötigen.  Der typische Fall für Windows ist Kerberos, bei dem eine Genauigkeit von 5 Minuten zwischen Client und Server erforderlich ist.  Es gibt jedoch viele weitere Bereiche, die von der Zeit Genauigkeit betroffen sein können, darunter:


- Behördliche Vorschriften wie:
    - 50 ms-Genauigkeit für FINRA in den USA
    - 1 MS ESMA (MiFID II) in der EU.
- Kryptografiealgorithmen
- Verteilte Systeme wie Cluster/SQL/Exchange und Dokument-DSB
- Blockchain-Framework für bitcoin-Transaktionen
- Verteilte Protokolle und Bedrohungsanalyse 
- AD-Replikation
- PCI (Payment Card Industry), zurzeit 1 Sekunde Genauigkeit



[!INCLUDE [windows-server-2016-improvements](windows-server-2016-improvements.md)]
