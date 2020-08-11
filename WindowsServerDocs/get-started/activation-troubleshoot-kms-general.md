---
title: Richtlinien zur Problembehandlung von KMS
description: Stellt Informationen zum KMS-Dienst bereit und schlägt Tools und Ansätze für die Behandlung von Aktivierungsproblemen vor.
ms.topic: troubleshooting
ms.date: 9/24/2019
author: Teresa-Motiv
ms.author: v-tea
manager: dcscontentpm
ms.localizationpriority: medium
ms.openlocfilehash: b31f357089ed54ed5f350657979740e7fd58651a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941808"
---
# <a name="guidelines-for-troubleshooting-the-key-management-service-kms"></a>Richtlinien für die Problembehandlung des Schlüsselverwaltungsdiensts (KMS)

Im Rahmen des Bereitstellungsprozesses richten viele Unternehmenskunden den Schlüsselverwaltungsdienst (Key Management Service, KMS) ein, um die Aktivierung von Windows in ihrer Umgebung zu ermöglichen. Hierbei handelt es sich um einen einfachen Prozess zum Einrichten des KMS-Hosts, nach dem die KMS-Clients den Host ermitteln und versuchen, sich eigenständig zu aktivieren. Was passiert jedoch, wenn dieser Prozess nicht funktioniert? Was ist dann der nächste Schritt? Dieser Artikel führt dich durch die Ressourcen, die du benötigst, um das Problem zu beheben. Weitere Informationen zu Ereignisprotokolleinträgen und dem Skript „Slmgr.vbs“ findest du unter [Technische Referenz zur Volumenaktivierung](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn502529(v=ws.11)).

## <a name="kms-overview"></a>KMS-Übersicht

Beginnen wir mit einer schnellen Auffrischung der KMS-Aktivierung. KMS ist ein Client/Server-Modell. Konzeptionell ähnelt es DHCP. Anstatt nach Anforderung durch Clients diesen IP-Adressen auszugeben, ermöglicht KMS die Produktaktivierung. KMS ist außerdem ein Erneuerungsmodell, in dem Clients versuchen, sich in regelmäßigen Abständen erneut zu aktivieren. Es gibt zwei Rollen: den *KMS-Host* und den *KMS-Client*.

- Der **KMS-Host** führt den Aktivierungsdienst aus und ermöglicht die Aktivierung in der Umgebung. Um einen KMS-Host zu konfigurieren, musst du einen KMS-Schlüssel aus dem Volume License Service Center (VLSC) installieren und dann den Dienst aktivieren.
- Der **KMS-Client** ist das Windows-Betriebssystem, das in der Umgebung bereitgestellt ist und aktiviert werden muss. KMS-Clients können eine beliebige Edition von Windows ausführen, die Volumenaktivierung verwendet. Die KMS-Clients werden mit einem vorinstallierten Schlüssel bereitgestellt, der als generischer Volumenlizenzschlüssel (Generic Volume License Key, GVLK,) bzw. KMS-Clientsetupschlüssel bezeichnet wird. Das Vorhandensein des GVLK macht aus einem System einen KMS-Client. Die KMS-Clients verwenden DNS-SRV-Einträge (_vlmcs._tcp), um den KMS-Host zu identifizieren. Die Clients versuchen dann automatisch, diesen Dienst zu ermitteln und zu verwenden, um sich selbst zu aktivieren. Während der standardmäßigen Karenzzeit von 30 Tagen versuchen sie alle zwei Stunden, sich zu aktivieren. Nach der Aktivierung versuchen die KMS-Clients alle sieben Tage, ihre Aktivierung zu erneuern.

Aus Gründen der Problembehandlung musst du möglicherweise beide Seiten (Host und Client) betrachten, um zu ermitteln, was vor sich geht.

## <a name="kms-host"></a>KMS-Host

Es gibt zwei zu untersuchende Bereiche auf dem KMS-Host. Überprüfe zunächst den Status des Softwarelizenzierungsdiensts auf dem Host. Überprüfe dann die Ereignisanzeige auf Ereignisse im Zusammenhang mit Lizenzierung oder Aktivierung.

### <a name="slmgrvbs-and-the-software-licensing-service"></a>„Slmgr.vbs“ und der Softwarelizenzierungsdienst

Um ausführliche Ausgaben vom Softwarelizenzierungsdienst zu erhalten, öffne ein Eingabeaufforderungsfenster mit erhöhten Rechten, und gib **slmgr.vbs /dlv** an der Eingabeaufforderung ein. Der folgende Screenshot zeigt die Ergebnisse dieses Befehls auf einem unserer KMS-Hosts innerhalb von Microsoft.

![Slmgr-Ausgabe auf KMS-Host](./media/ee939272.kms_slmgr_output(en-us,technet.10).png)

Die wichtigsten Felder für die Problembehandlung sind die folgenden. Wonach du genau suchst, kann abhängig von dem zu lösenden Problem variieren.

- **Versionsinformationen**. Am Anfang der Ausgabe von **slmgr.vbs /dlv** befindet sich die Version des Softwarelizenzierungsdiensts. Dies kann hilfreich sein, um zu bestimmen, ob die aktuelle Version des Diensts installiert ist. Beispielsweise unterstützen Updates des KMS-Diensts unter Windows Server 2003 unterschiedliche KMS-Hostschlüssel. Diese Daten können verwendet werden, um zu bewerten, ob die Version aktuell ist oder nicht und den KMS-Hostschlüssel unterstützt, den du installieren möchtest. Weitere Informationen zu diesen Updates findest du unter [Ein verfügbares Update für Windows Vista und Windows Server 2008 erweitert KMS-Aktivierungsunterstützung für Windows 7 und Windows Server 2008 R2 ](https://support.microsoft.com/help/968912/an-update-is-available-for-windows-vista-and-for-windows-server-2008-t).
- **Name**: Dies zeigt die Edition von Windows an, die auf dem KMS-Hostsystem installiert ist. Dies kann für die Problembehandlung wichtig sein, wenn du Probleme beim Hinzufügen oder Ändern des KMS-Hostschlüssels hast (z. B. um zu überprüfen, ob der Schlüssel von dieser Betriebssystemversion unterstützt wird).
- **Beschreibung** Hier wird der Schlüssel angezeigt, der installiert ist. Verwende dieses Feld, um zu überprüfen, welcher Schlüssel verwendet wurde, um den Dienst zu aktivieren, und ob dies der richtige für die von dir bereitgestellten KMS-Clients ist.
- **Lizenzstatus**. Dies ist der Status des KMS-Hostsystems. Der Wert sollte **Lizenziert** lauten. Jeder andere Wert bedeutet, dass etwas falsch ist und dass du den Host möglicherweise erneut aktivieren musst.
- **Aktuelle Anzahl**. Die angezeigte Anzahl liegt zwischen **0** und **50**. Die Anzahl ist kumulativ (zwischen Betriebssystemen) und gibt die Anzahl gültiger Systeme an, die innerhalb eines Zeitraums von 30 Tagen versucht haben, sich zu aktivieren.

  Wenn die Anzahl **0** ist, wurde der Dienst entweder kürzlich aktiviert, oder es sind keine gültigen Clients mit dem KMS-Host verbunden.

  Die Anzahl steigt nicht über **50**, unabhängig davon, wie viele gültige Systeme in der Umgebung vorhanden sind. Dies liegt daran, dass die Anzahl darauf festgelegt ist, nur das Doppelte der maximalen Lizenzrichtlinie zwischenzuspeichern, die von einem KMS-Client zurückgegeben wird. Die maximale Richtlinie wird heute vom Windows-Clientbetriebssystem festgelegt, das eine Anzahl von **25** oder höher vom KMS-Host erfordert, um sich selbst zu aktivieren. Daher beträgt die höchste Anzahl auf dem KMS-Host 2 x 25, also 50. Beachte, dass in Umgebungen, die nur Windows Server-KMS-Clients enthalten, die maximale Anzahl auf dem KMS-Host **10** ist. Dies liegt daran, dass der Schwellenwert für die Windows Server-Editionen **5** (2 x 5, also 10) ist.

  Ein häufiges Problem, das sich auf die Anzahl bezieht, besteht darin, dass die Umgebung über einen aktivierten KMS-Host und eine ausreichende Anzahl von Clients verfügt, die Anzahl jedoch nicht auf mehr als 1 erhöht wird. Das Hauptproblem besteht darin, dass das bereitgestellte Clientimage nicht korrekt konfiguriert wurde (**sysprep /generalize**) und dass die Systeme keine eindeutigen Clientcomputer-IDs (CMIDs) verfügen. Weitere Informationen findest du unter [KMS-Client](#kms-client) und [Die aktuelle KMS-Anzahl erhöht sich nicht, wenn Sie neue Windows Vista- oder Windows 7-basierte Clientcomputer im Netzwerk hinzufügen](https://support.microsoft.com/help/929829/the-kms-current-count-does-not-increase-when-you-add-new-windows-vista). Einer unserer Supporteskalationstechniker hat auch in einem Blog zu diesem Thema geschrieben unter [KMS Host Client Count not Increasing Due to Duplicate CMID’S](/archive/blogs/askcore/kms-host-client-count-not-increasing-due-to-duplicate-cmids).

  Ein weiterer Grund, warum die Anzahl möglicherweise nicht zunimmt, liegt darin, dass zu viele KMS-Hosts in der Umgebung vorhanden sind und die Anzahl über alle verteilt wird.
- **Lauschen am Port**. Bei der Kommunikation mit KMS werden anonyme Remoteprozeduraufrufe (RPC) verwendet. Standardmäßig verwenden die Clients den TCP-Port 1688, um eine Verbindung mit dem KMS-Host herzustellen. Stelle sicher, dass dieser Port zwischen deinen KMS-Clients und dem KMS-Host geöffnet ist. Du kannst den Port auf dem KMS-Host ändern oder konfigurieren. Während der Kommunikation sendet der KMS-Host die Portfestlegung an die KMS-Clients. Wenn du den Port auf einem KMS-Client änderst, wird die Portfestlegung überschrieben, wenn dieser Client den Host kontaktiert.

Häufig erhalten wir Fragen zu dem Abschnitt „Kumulative Anforderungen“ der Ausgabe von **slmgr.vbs /dlv**. Diese Daten sind im Allgemeinen nicht hilfreich bei der Problembehandlung. Der KMS-Host pflegt einen fortlaufenden Datensatz des Zustands jedes KMS-Clients, der versucht, sich zu aktivieren oder erneut zu aktivieren. Fehlerhafte Anforderungen weisen auf KMS-Clients hin, die vom KMS-Host nicht unterstützt werden. Wenn z. B. ein Windows 7-KMS-Client versucht, sich bei einem KMS-Host zu aktivieren, der mithilfe eines Windows Vista KMS-Schlüssels aktiviert wurde, schlägt die Aktivierung fehl. In der Zeile „Anforderungen mit Lizenzstatus“ werden alle möglichen Lizenzzustände, vergangene und aktuelle, beschrieben. Aus Gründen der Problembehandlung sind diese Daten nur dann relevant, wenn die Anzahl nicht erwartungsgemäß zunimmt. In diesem Fall sollte sich die Anzahl der fehlgeschlagenen Anforderungen erhöhen. Dies deutet darauf hin, dass du den Product Key überprüfen solltest, der zum Aktivieren des KMS-Hostsystems verwendet wurde. Beachte außerdem, dass die kumulierten Anforderungswerte nur zurückgesetzt werden, wenn du das KMS-Hostsystem neu installierst.

### <a name="useful-kms-host-events"></a>Nützliche KMS-Host-Ereignisse

#### <a name="event-id-12290"></a>Ereignis-ID 12290

Der KMS-Host protokolliert die Ereignis-ID 12290, wenn ein KMS-Client den Host kontaktiert, um sich zu aktivieren. Die Ereignis-ID 12290 enthält eine beträchtliche Menge an Informationen, die du verwenden kannst, um herauszufinden, welche Art von Client den Host kontaktiert hat und warum ein Fehler aufgetreten ist. Das folgende Segment eines Ereignis-ID 12290-Eintrags stammt aus dem Ereignisprotokoll des Schlüsselverwaltungsdiensts des KMS-Hosts.

![KMS-Ereignis 12290](./media/ee939272.kms_12290_event(en-us,technet.10).png)

Die Ereignisdetails enthalten die folgenden Informationen:

- **Zur Aktivierung erforderliche Mindestanzahl**. Der KMS-Client meldet, dass die Anzahl vom KMS-Host **5** sein muss, um aktiviert zu werden. Dies bedeutet, dass dies ein Windows Server-Betriebssystem ist, obwohl keine bestimmte Edition angegeben wird. Wenn deine Clients nicht aktiviert werden, stelle sicher, dass die Anzahl auf dem Host ausreichend ist.
- **Clientcomputer-ID (CMID)** . Dies ist ein eindeutiger Wert für jedes System. Wenn dieser Wert nicht eindeutig ist, liegt dies daran, dass ein Image nicht ordnungsgemäß für die Verteilung vorbereitet wurde (**sysprep /generalize**). Dieses Problem tritt auf dem KMS-Host als Anzahl auf, die sich nicht erhöht, auch wenn genügend Clients in der Umgebung vorhanden sind. Weitere Informationen findest du unter [Die aktuelle KMS-Anzahl erhöht sich nicht, wenn Sie neue Windows Vista- oder Windows 7-basierte Clientcomputer im Netzwerk hinzufügen](https://support.microsoft.com/help/929829/the-kms-current-count-does-not-increase-when-you-add-new-windows-vista).
- **Lizenzstatus und Zeit bis zum Ablauf des Zustands**. Dies ist der aktuelle Lizenzstatus des Clients. Er kann bei der Unterscheidung eines Clients helfen, der zum ersten Mal versucht, sich zu aktivieren, von einem Client, der sich erneut aktivieren möchte. Der Zeiteintrag gibt Aufschluss darüber, wie viel länger der Client in diesem Zustand verbleiben wird, wenn sich nichts ändert.

Wenn du eine Problembehandlung für einen Client ausführst und keine entsprechende Ereignis-ID 12290 auf dem KMS-Host finden kannst, stellt dieser Client keine Verbindung mit dem KMS-Host her. Einige Gründe, warum ein Eintrag der Ereignis-ID 12290 möglicherweise nicht vorhanden ist, lauten wie folgt:

- Ein Netzwerkausfall ist aufgetreten.
- Der Host wird im DNS nicht aufgelöst oder ist dort nicht registriert.
- Die Firewall blockiert TCP 1688.
   Der Port könnte an vielen Stellen innerhalb der Umgebung blockiert werden, auch auf dem KMS-Hostsystem selbst. Standardmäßig ist auf dem KMS-Host eine Firewallausnahme für KMS vorhanden, aber diese wird nicht automatisch aktiviert. Du musst die Ausnahme explizit aktivieren.
- Das Ereignisprotokoll ist voll.

KMS-Clients protokollieren zwei korrespondierende Ereignisse, Ereignis-ID 12288 und Ereignis-ID 12289. Informationen zu diesen Ereignissen findest du im Abschnitt [KMS-Client](#kms-client).

#### <a name="event-id-12293"></a>Ereignis-ID 12293

Ein weiteres relevantes Ereignis, nach dem du auf deinem KMS-Host suchen solltest, ist die Ereignis-ID 12293. Dieses Ereignis zeigt an, dass der Host die erforderlichen Einträge nicht im DNS veröffentlicht hat. Diese Situation führt bekanntermaßen zu Fehlern und sollte von dir überprüft werden, *nachdem* du deinen Host eingerichtet hast, und *bevor* du Clients bereitstellst. Weitere Informationen zu DNS-Problemen findest du unter [Allgemeine Verfahren zum Behandeln von KMS- und DNS-Problemen](common-troubleshooting-procedures-kms-dns.md).

## <a name="kms-client"></a>KMS-Client

Auf den Clients verwendest du dieselben Tools (Slmgr und Ereignisanzeige) zur Problembehandlung der Aktivierung.

### <a name="slmgrvbs-and-the-software-licensing-service"></a>„Slmgr.vbs“ und der Softwarelizenzierungsdienst

Um ausführliche Ausgaben vom Softwarelizenzierungsdienst zu erhalten, öffne ein Eingabeaufforderungsfenster mit erhöhten Rechten, und gib **slmgr.vbs /dlv** an der Eingabeaufforderung ein. Der folgende Screenshot zeigt die Ergebnisse dieses Befehls auf einem unserer KMS-Hosts innerhalb von Microsoft.

![Slmgr-Ausgabe auf KMS-Client](./media/ee939272.kms_client_slmgr_output(en-us,technet.10).png)

Die folgende Liste umfasst die wichtigsten Felder für die Problembehandlung. Wonach du genau suchst, kann abhängig von dem zu lösenden Problem variieren.

- **Name**: Dieser Wert ist die Edition von Windows, die auf dem KMS-Clientsystem installiert ist. Verwende diesen Wert, um zu überprüfen, ob die Windows-Version, die du aktivieren möchtest, KMS verwenden kann. Unser Helpdesk hat beispielsweise Vorfälle gesehen, in denen Kunden versuchen, den KMS-Clientsetupschlüssel in einer Windows-Edition zu installieren, die keine Volumenaktivierung verwendet, wie z. B. Windows Vista Ultimate.
- **Beschreibung** Dieser Wert zeigt den Schlüssel an, der installiert ist. VOLUME_KMSCLIENT gibt an, dass der KMS-Clientsetupschlüssel (oder GVLK) installiert ist (die Standardkonfiguration für Volumenlizenzmedien) und dass dieses System automatisch versucht, sich mithilfe eines KMS-Hosts zu aktivieren. Wenn hier etwas anderes angezeigt wird, z. B. MAK, musst du den GVLK neu installieren, um dieses System als KMS-Client zu konfigurieren. Du kannst den Schlüssel manuell installieren, indem du **slmgr.vsb /ipk&lt;*GVLK*&gt;** (wie in [KMS-Clientsetupschlüssel](kmsclientkeys.md) beschrieben) oder das Tool zur Verwaltung der Volumenaktivierung (VAMT) verwendest. Weitere Informationen, wie du das VAMT abrufen und verwenden kannst, findest du unter [Technische Referenz zum Tool für die Verwaltung der Volumenaktivierung (Volume Activation Management Tool, VAMT)](/windows/deployment/volume-activation/volume-activation-management-tool).
- **Product Key (teilweise)** . Als Feld **Name** kannst du diese Information verwenden, um zu bestimmen, ob der richtige KMS-Clientsetupschlüssel auf diesem Computer installiert ist (mit anderen Worten, ob der Schlüssel dem Betriebssystem entspricht, das auf dem KMS-Client installiert ist). Standardmäßig ist der richtige Schlüssel auf Systemen vorhanden, die mithilfe von Medien aus dem Volume License Service Center-Portal (VLSC) erstellt wurden. In einigen Fällen können Kunden die Aktivierung mit Mehrfachaktivierungsschlüssel (MAK) verwenden, bis in der Umgebung genügend Systeme vorhanden sind, um die KMS-Aktivierung zu unterstützen. Der KMS-Clientsetupschlüssel muss auf diesen Systemen installiert sein, um sie von MAK auf KMS umzustellen. Verwende das VAMT, um diesen Schlüssel zu installieren und sicherzustellen, dass der richtige Schlüssel angewendet ist.
- **Lizenzstatus**. Dieser Wert zeigt den Status des KMS-Clientsystems an. Bei einem System, das mit KMS aktiviert wurde, sollte dieser Wert **Lizenziert** lauten. Jeder andere Wert weist möglicherweise darauf hin, dass ein Problem vorliegt. Wenn z. B. der KMS-Host ordnungsgemäß funktioniert und der KMS-Client nicht aktiviert ist (z. B. verbleibt er in einem **Karenz**zustand), verhindert möglicherweise ein Umstand, dass der Client das Hostsystem erreicht (beispielsweise ein Firewallproblem, ein Netzwerkausfall oder etwas ähnliches).
- **Clientcomputer-ID (CMID)** . Jeder KMS-Client muss eine eindeutige CMID besitzen. Wie bereits im Abschnitt [KMS-Host](#kms-host) erwähnt, besteht ein häufiges Problem, das sich auf die Anzahl bezieht, darin, dass die Umgebung über einen aktivierten KMS-Host und eine ausreichende Anzahl von Clients verfügt, die Anzahl jedoch nicht auf mehr als **1** erhöht wird. Weitere Informationen findest du unter [Die aktuelle KMS-Anzahl erhöht sich nicht, wenn Sie neue Windows Vista- oder Windows 7-basierte Clientcomputer im Netzwerk hinzufügen](https://support.microsoft.com/help/929829/the-kms-current-count-does-not-increase-when-you-add-new-windows-vista).
- **KMS-Computername aus DNS**. Dieser Wert zeigt den vollqualifizierten Namen (FQDN) des KMS-Hosts an, den der Client erfolgreich für die Aktivierung verwendet hat, sowie den für die Kommunikation verwendeten TCP-Port.
- **KMS-Hostzwischenspeicherung**. Der endgültige Wert zeigt an, ob Zwischenspeicherung aktiviert ist oder nicht. Standardmäßig ist sie aktiviert. Dies bedeutet, dass der KMS-Client den Namen des KMS-Hosts zwischenspeichert, der für die Aktivierung verwendet wird, und dass er direkt mit diesem Host kommuniziert (anstatt das DNS abzufragen), wenn er erneut aktiviert werden muss. Wenn der Client den zwischengespeicherten KMS-Host nicht kontaktieren kann, fragt er das DNS ab, um einen neuen KMS-Host zu ermitteln.

### <a name="useful-kms-client-events"></a>Nützliche KMS-Client-Ereignisse

#### <a name="event-id-12288-and-event-id-12289"></a>Ereignis-ID 12288 und Ereignis-ID 12289

Wenn sich ein KMS-Client erfolgreich aktiviert oder erneut aktiviert, protokolliert der Client zwei Ereignisse: Ereignis-ID 12288 und Ereignis-ID 12289. Das folgende Segment eines Ereignis-ID 12288-Eintrags stammt aus dem Ereignisprotokoll des Schlüsselverwaltungsdiensts unseres KMS-Clients.

![KMS-Client-Ereignis-ID 12288](./media/ee939272.client_12288(en-us,technet.10).png)

Wenn nur die Ereignis-ID 12288 (ohne die entsprechende Ereignis-ID 12289) angezeigt wird, bedeutet dies, dass der KMS-Client den KMS-Host nicht erreichen konnte, der KMS-Host nicht geantwortet hat, oder der Client keine Antwort empfangen hat. Vergewissere dich in diesem Fall, dass der KMS-Host ermittelt werden kann und dass die KMS-Clients ihn kontaktieren können.

Die relevantesten Informationen in der Ereignis-ID 12288 sind die Daten im Abschnitt „Info“. In diesem Abschnitt werden z. B. der aktuelle Zustand des Clients sowie der FQDN und der TCP-Port angezeigt, die vom Client beim Versuch der Aktivierung verwendet wurden. Du kannst den FQDN verwenden, um Problemfälle zu beheben, bei denen die Anzahl auf einem KMS-Host nicht zunimmt. Wenn z. B. den Clients (entweder legitimen oder nicht autorisierte Systeme) zu viele KMS-Hosts zur Verfügung stehen, wird die Anzahl möglicherweise über alle verteilt.

Eine nicht erfolgreiche Aktivierung bedeutet nicht immer, dass der Client 12288, aber nicht 12289 aufweist. Bei einer fehlgeschlagenen Aktivierung oder erneuten Aktivierung können auch beide Ereignisse vorhanden sein. In diesem Fall musst du das zweite Ereignis überprüfen, um den Grund für den Fehler zu überprüfen.

![KMS-Client-Ereignis-ID 12289](./media/ee939272.client_12289(en-us,technet.10).png)

Der Abschnitt „Info“ von Ereignis-ID 12289 enthält folgende Informationen:

- **Aktivierungsflag**. Dieser Wert zeigt an, ob die Aktivierung erfolgreich war (**1**) oder fehlgeschlagen (**0**) ist.
- **Aktuelle Anzahl auf dem KMS-Host**. Dieser Wert gibt den Wert der Anzahl auf dem KMS-Host an, wenn der Client versucht, sich zu aktivieren. Wenn die Aktivierung fehlschlägt, kann dies daran liegen, dass die Anzahl für dieses Clientbetriebssystem unzureichend ist oder dass in der Umgebung nicht genügend Systeme zum Erzielen der Anzahl vorhanden sind.

## <a name="what-does-support-ask-for"></a>Wonach fragt der Support?

Wenn du den Support anrufen musst, um eine Problembehandlung bei der Aktivierung durchzuführen, fordert der Supporttechniker in der Regel die folgenden Informationen an:

- **Slmgr.vbs**-Ausgabe des KMS-Hosts und der KMS-Clientsysteme. Unabhängig davon, ob du den Befehl mit „wscript“ oder „cscript“ ausführst, kannst du die Ausgabe mithilfe von STRG+C kopieren und dann in Editor einfügen, um sie an den Supportkontakt zu senden.
- Ereignisprotokolle sowohl vom KMS-Host (Schlüsselverwaltungsdienst-Protokoll) und den KMS-Clientsystemen (Anwendungsprotokoll).

## <a name="additional-references"></a>Weitere Verweise
- [Ask the Core Team: #Activation](/archive/blogs/askcore/kms-host-client-count-not-increasing-due-to-duplicate-cmids)
