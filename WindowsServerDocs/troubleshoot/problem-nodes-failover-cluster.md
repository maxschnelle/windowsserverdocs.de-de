---
title: Ein Problem beim Löschen eines Knotens.
description: Dieser Artikel beschreibt die Probleme, die beim Entfernen von Knoten aus der aktiven failoverclustermitgliedschaft aufgetreten sind.
ms.prod: windows-server
ms.technology: server-general
ms.date: 05/28/2020
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 30714e8a9c5ca4ad13ed6757c6ce1da211b279ac
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150228"
---
# <a name="having-a-problem-with-nodes-being-removed-from-active-failover-cluster-membership"></a>Probleme mit Knoten, die aus der Mitgliedschaft des aktiven Failoverclusters entfernt wurden

In diesem Artikel wird beschrieben, wie Sie Probleme beheben, bei denen Knoten zufällig aus der aktiven failoverclustermitgliedschaft entfernt werden.

## <a name="symptoms"></a>Symptome

Wenn das Problem auftritt, sehen Sie, dass Ereignisse wie diese in Ihrem System Ereignisprotokoll protokolliert werden:

![Ereignis 1135](media/problem-nodes-failover-cluster/1135-1.png)

Dieses Ereignis wird auf allen Knoten im Cluster protokolliert, ausgenommen dem Knoten, der entfernt wurde. Der Grund für dieses Ereignis ist, dass einer der Knoten im Cluster den Knoten als "herunter" markiert hat. Anschließend werden alle anderen Knoten des Ereignisses benachrichtigt. Wenn die Knoten benachrichtigt werden, brechen Sie Ihre Takt Verbindungen mit dem untergeordneten Knoten ab und brechen Sie ab.

## <a name="what-caused-the-node-to-be-marked-down"></a>Was hat bewirkt, dass der Knoten markiert ist

Alle Knoten in einem Windows 2008-oder 2008 R2-Failovercluster kommunizieren miteinander über die Netzwerke, die für die Netzwerkkommunikation im Netzwerk in diesem Netzwerk festgelegt sind. Die Knoten senden Takt Pakete über diese Netzwerke an alle anderen Knoten. Diese Pakete sollen von den anderen Knoten empfangen werden, und anschließend wird eine Antwort zurückgesendet. Jeder Knoten im Cluster weist seine eigenen Takte auf, die überwacht werden, um sicherzustellen, dass das Netzwerk aktiv ist und die anderen Knoten aktiv sind. Das folgende Beispiel sollte Ihnen helfen, dies zu verdeutlichen:

![Nodes](media/problem-nodes-failover-cluster/Node2.png)

Wenn keines dieser Pakete zurückgegeben wird, wird der jeweilige Takt als fehlerhaft betrachtet. Beispielsweise sendet W2K8-R2-Node2 eine Anforderung und empfängt eine Antwort von W2K8-R2-Node1 an ein Takt Paket, damit das Netzwerk bestimmt wird und der Knoten aktiv ist.  Wenn W2K8-R2-Node1 eine Anforderung an W2K8-R2-Node2 sendet und W2K8-R2-Node1 die Antwort nicht erhält, wird Sie als verlorener Takt angesehen, und W2K8-R2-Node1 verfolgt Sie nach.  Diese verpasste Antwort kann W2K8-R2-Node1 das Netzwerk anzeigen, bis eine andere Takt Anforderung empfangen wird.

Standardmäßig sind für Cluster Knoten fünf Fehler in 5 Sekunden festgelegt, bevor die Verbindung markiert wird. Wenn W2K8-R2-Node1 die Antwort nicht fünfmal im Zeitraum empfängt, wird diese bestimmte Route als "W2K8-R2-Node2" betrachtet. Wenn andere Routen weiterhin als aktiv angesehen werden, bleibt W2K8-R2-Node2 als aktives Mitglied.

Wenn alle Routen für W2K8-R2-Node2 gekennzeichnet sind, werden Sie aus der aktiven failoverclustermitgliedschaft entfernt. das Ereignis 1135, das Sie im ersten Abschnitt sehen, wird protokolliert. Auf W2K8-R2-Node2 wird der Cluster Dienst beendet und dann neu gestartet, damit versucht wird, den Cluster erneut beizutreten.

Weitere Informationen zur Handhabung bestimmter Routen mit drei oder mehr Knoten finden Sie im Blog ["partitionierte" Cluster Netzwerke](/archive/blogs/askcore/partitioned-cluster-networks) , der von Jeff Hughes geschrieben wurde.

## <a name="now-that-we-know-how-the-heartbeat-process-works-what-are-some-of-the-known-causes-for-the-process-to-fail"></a>Nachdem wir nun wissen, wie der Takt Prozess funktioniert, sind einige der bekannten Gründe für einen fehlerhaften Prozess zu erkennen.

1. Tatsächliche Netzwerkhardware Fehler. Wenn das Paket bei der Übertragung irgendwo zwischen den Knoten verloren geht, schlagen die Takte fehl. Dies wird durch eine Netzwerk Ablauf Verfolgung von beiden beteiligten Knoten offengelegt.

2. Das Profil für Ihre Netzwerkverbindungen kann möglicherweise erneut von Domäne zu öffentlich und wieder zurück in die Domäne überspringt werden. Während des Übergangs dieser Änderungen kann die Netzwerk-e/a blockiert werden. Sie können überprüfen, ob dies der Fall ist, indem Sie sich das Netzwerk Profil des Betriebs Protokolls ansehen. Sie finden dieses Protokoll durch Öffnen des Ereignisanzeige und navigieren zu: Anwendungs-und dienstprotokolle\microsoft\windows\networkprofile\operational. Sehen Sie sich die Ereignisse in diesem Protokoll auf dem Knoten an, der in der Ereignis-ID: 1135 erwähnt wurde, und überprüfen Sie, ob das Profil zu diesem Zeitpunkt geändert wurde. Wenn dies der Fall ist, lesen Sie den KB-Artikel [Netzwerkadressen Profile von "Domäne" in "öffentlich" in Windows 7 oder in Windows Server 2008 R2](https://support.microsoft.com/help/2524478/the-network-location-profile-changes-from-domain-to-public-in-windows).

3. Auf den Servern ist IPv6 aktiviert, aber die folgenden beiden Regeln sind für eingehende und ausgehende Daten in der Windows-Firewall deaktiviert:

    - Kern Netzwerk-Nachbar Ermittlungs Ankündigung
    - Kern Netzwerk-Nachbar Ermittlungs Anfrage

4. Die Antivirussoftware könnte diesen Prozess ebenfalls beeinträchtigen. Wenn Sie dies vermuten, testen Sie die Software, indem Sie Sie deaktivieren oder deinstallieren. Führen Sie dies auf eigene Gefahr aus, da Sie an diesem Punkt nicht gegen Viren geschützt werden.

5. Dies kann auch dazu führen, dass die Latenz in Ihrem Netzwerk auftritt. Die Pakete können zwischen den Knoten nicht verloren gehen, Sie werden jedoch möglicherweise nicht schnell genug auf die Knoten übergegangen, bevor das Timeout abläuft.

6. IPv6 ist das Standardprotokoll, das von Failoverclustering für die Takte verwendet wird. Der Heartbeat selbst ist ein UDP-unicastnetzwerkpaket, das über Port 3343 kommuniziert. Wenn Switches, Firewalls oder Router nicht ordnungsgemäß konfiguriert sind, um diesen Datenverkehr durch zuzulassen, können Probleme wie diese auftreten.

7. Diese Probleme können auch durch IPSec-Sicherheitsrichtlinien aktualisiert werden. Das besondere Problem besteht darin, dass während der Aktualisierung der IPSec-Gruppenrichtlinie alle IPSec-Sicherheits Zuordnungen (SAS) von der Windows-Firewall mit erweiterter Sicherheit (wfas) abgebrochen werden. In diesem Fall wird die gesamte Netzwerk Konnektivität blockiert. Wenn beim Durchführen der Authentifizierung mit Active Directory Verzögerungen beim Durchführen der Sicherheits Zuordnungen auftreten, blockieren diese Verzögerungen (bei denen die gesamte Netzwerkkommunikation blockiert ist) auch die Durchführung von Cluster Takten und bewirken, dass die Cluster Integritäts Überwachung Knoten als instand erkennt, wenn Sie nicht innerhalb des Schwellenwerts von 5 Sekunden reagieren.

8. Alte oder veraltete Netzwerkkarten Treiber und/oder Firmware.  Manchmal kann eine einfache Fehlkonfiguration der Netzwerkkarte oder des Schalters auch zu einem Verlust von Takten führen.

9. Bei modernen Netzwerkkarten und virtuellen Netzwerkkarten ist möglicherweise ein Paketverlust aufgetreten.  Dies kann nachverfolgt werden, indem Sie den System Monitor öffnen und den Leistungsindikatoren "Netzwerkschnittstelle\Empfangene Pakete" hinzufügen.  Dieser Wert ist kumulativ und wird nur erhöht, bis der Server neu gestartet wird.  Eine große Anzahl von Paketen, die hier abgelegt werden, könnte ein Vorzeichen dafür sein, dass die Empfangs Puffer auf der Netzwerkkarte zu niedrig festgelegt sind oder der Server langsam funktioniert und den eingehenden Datenverkehr nicht verarbeiten kann.  Jeder Netzwerkkarten Hersteller entscheidet, ob diese Einstellungen in den Eigenschaften der Netzwerkkarte verfügbar gemacht werden. Daher müssen Sie auf die Website des Herstellers verweisen, um zu erfahren, wie Sie diese Werte erhöhen und die empfohlenen Werte verwenden.  Wenn Sie auf VMware ausführen, wird im folgenden Blog ausführlicher erläutert, wie Sie feststellen können, ob dies das Problem ist, und Sie werden auf den VMware-Artikel zu den zu ändernden Einstellungen verwiesen.

    [Knoten, die aus der failoverclustermitgliedschaft in VMware ESX entfernt werden](/archive/blogs/askcore/nodes-being-removed-from-failover-cluster-membership-on-vmware-esx)

Dies sind die häufigsten Gründe, aus denen diese Ereignisse protokolliert werden, aber es kann auch andere Gründe geben. Der Punkt dieses Blogs war, Ihnen einen Einblick in den Prozess zu vermitteln und außerdem Ideen dazu zu vermitteln, was Sie suchen sollten. Von einigen werden die folgenden Werte auf die maximalen Werte angehoben, um zu versuchen, dieses Problem zu verhindern.

|Parameter|Standard|Bereich|
|---|---|---|
|**SameSubnetDelay**|1000 Millisekunden|250-2000 Millisekunden|
|**CrossSubnetDelay**|1000 Millisekunden|250-4000 Millisekunden|
|**SameSubnetThreshold**|5|3-10|
|**CrossSubnetThreshold**|5|3-10|
||||

Wenn Sie diese Werte auf den maximalen Wert erhöhen, wird das Entfernen von Ereignis und Knoten möglicherweise entfernt, und das Problem wird lediglich maskiert. Das Problem kann nicht behoben werden. Das beste daran ist, die Grundursache der Takt Ausfälle zu finden und diese festzulegen. Die einzige wirkliche Notwendigkeit, diese Werte zu erhöhen, liegt in einem Szenario mit mehreren Standorten, bei dem sich Knoten an unterschiedlichen Standorten befinden und die Netzwerk Latenz nicht umgangen werden kann.
