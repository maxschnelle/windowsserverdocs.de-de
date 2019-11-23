---
ms.assetid: d1953097-63ea-4a0e-b860-2f3b7c175c41
title: Funktionsweise des Windows-Zeitdiensts
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 2bf4a887218cd51e9c10954a75bbc1ba2112647f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405143"
---
# <a name="how-the-windows-time-service-works"></a>Funktionsweise des Windows-Zeitdiensts

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

**In diesem Abschnitt**  
  
-   [Windows-Zeit Dienst Architektur](#windows-time-service-architecture)  
  
-   [Windows-Zeit Dienstnutzungsdauer Protokolle](#windows-time-service-time-protocols)  
  
-   [Windows-Zeit Dienst Prozesse und-Interaktionen](#windows-time-service-processes-and-interactions)  
  
-   [Vom Windows-Zeit Dienst verwendete Netzwerkports](#network-ports-used-by-windows-time-service)  
  
> [!NOTE]  
> In diesem Thema wird nur erläutert, wie der Windows-Zeit Dienst (W32Time) funktioniert. Informationen zum Konfigurieren des Windows-Zeit diensdienstanbieter finden Sie unter [Konfigurieren von Systemen für hohe Genauigkeit](configuring-systems-for-high-accuracy.md).
  
> [!NOTE]  
> In Windows Server 2003 und Microsoft Windows 2000 Server wird der Verzeichnisdienst Active Directory Verzeichnisdienst benannt. In Windows Server 2008 und höheren Versionen wird der Verzeichnisdienst Active Directory Domain Services (AD DS) benannt. Im weiteren Verlauf dieses Themas wird Bezug auf AD DS genommen, die Informationen gelten jedoch auch für Active Directory.  
  
Obwohl es sich bei dem Windows-Zeit Dienst nicht um eine exakte Implementierung des Netzwerk Zeit Protokolls (Network Time Protocol, NTP) handelt, verwendet er die komplexe Suite von Algorithmen, die in den NTP-Spezifikationen definiert sind, um sicherzustellen, dass Uhren auf Computern innerhalb eines Netzwerks so genau wie möglich sind. Im Idealfall werden alle Computeruhren in einer AD DS Domäne mit dem Zeitpunkt eines autorisierenden Computers synchronisiert. Viele Faktoren können sich auf die Zeitsynchronisierung in einem Netzwerk auswirken. Die folgenden Faktoren wirken sich häufig auf die Genauigkeit der Synchronisierung in AD DS aus:  
  
-   Netzwerkbedingungen  
  
-   Die Genauigkeit der Hardware Uhr des Computers  
  
-   Die Menge an CPU-und Netzwerkressourcen, die für den Windows-Zeit Dienst verfügbar sind  
  
> [!IMPORTANT]  
> Vor Windows Server 2016 wurde der W32Time-Dienst nicht so konzipiert, dass er Zeit empfindliche Anwendungsanforderungen erfüllt.  Updates für Windows Server 2016 ermöglichen es Ihnen jetzt jedoch, eine Lösung für eine Genauigkeit von 1 MS in Ihrer Domäne zu implementieren.  Weitere Informationen finden Sie unter [Windows 2016 (genaue Zeit](accurate-time.md) -und [Support Grenze) zum Konfigurieren des Windows-Zeit diensdienstanbieter für Umgebungen mit hoher Genauigkeit](support-boundary.md) .  
  
Computer, die Ihre Zeit seltener synchronisieren oder nicht mit einer Domäne verbunden sind, werden standardmäßig so konfiguriert, dass Sie mit Time.Windows.com synchronisiert werden.  Daher ist es nicht möglich, die Zeit Genauigkeit auf Computern zu gewährleisten, die über vorübergehende oder keine Netzwerkverbindungen verfügen.  
  
Eine AD DS-Gesamtstruktur verfügt über eine vorgegebene Zeit Synchronisierungs Hierarchie. Der Windows-Zeit Dienst synchronisiert die Zeit zwischen den Computern innerhalb der Hierarchie mit den genauesten Verweis Uhren im oberen Bereich. Wenn auf einem Computer mehr als eine Zeit Quelle konfiguriert ist, verwendet die Windows-Zeit NTP-Algorithmen, um die beste Zeit Quelle aus den konfigurierten Quellen auszuwählen, und zwar basierend auf der Fähigkeit des Computers, eine Synchronisierung mit dieser Zeit Quelle durchzusetzen. Der Windows-Zeit Dienst unterstützt keine Netzwerk Synchronisierung von Broadcast-oder Multicast Peers. Weitere Informationen zu diesen NTP-Funktionen finden Sie unter RFC 1305 in der IETF RFC-Datenbank.  
  
Auf allen Computern, auf denen der Windows-Zeit Dienst ausgeführt wird, wird der-Dienst verwendet, um den genauesten Zeitpunkt beizubehalten. Computer, die Mitglieder einer Domäne sind, fungieren standardmäßig als Zeit Client. in den meisten Fällen ist es daher nicht erforderlich, den Windows-Zeit Dienst zu konfigurieren. Der Windows-Zeit Dienst kann jedoch so konfiguriert werden, dass er Zeit von einer bestimmten Verweis Zeit Quelle anfordert und auch Zeit für Clients bereitstellt.
  
Der Grad, zu dem die Zeit eines Computers genau ist, wird als Stratum bezeichnet. Die genaueste Zeit Quelle in einem Netzwerk (z. b. eine Hardwareuhr) belegt die niedrigste straterstufe (Stratum eins). Diese genaue Zeit Quelle wird als Referenzuhr bezeichnet. Ein NTP-Server, der seine Zeit direkt von einer verweisuhr erhält, belegt einen Stratum, der eine höhere Ebene als die der Referenzuhr ist. Ressourcen, die Zeit vom NTP-Server abrufen, sind zwei Schritte von der Referenzuhr. Sie belegen daher einen Stratum, der zwei über der genauesten Zeit Quelle ist, usw. Wenn die Stratum-Nummer eines Computers zunimmt, kann die Systemuhr Zeit weniger genau werden. Daher ist die Stratum-Ebene eines beliebigen Computers ein Indikator dafür, wie genau der Computer mit der genauesten Zeit Quelle synchronisiert wird.  
  
Wenn der W32Time-Manager Zeit Beispiele empfängt, verwendet er besondere Algorithmen in NTP, um zu bestimmen, welche der Zeit Proben am besten geeignet ist. Der Zeit Dienst verwendet auch einen anderen Satz von Algorithmen, um zu bestimmen, welche der konfigurierten Zeitquellen am genauesten ist. Wenn der Zeit Dienst festgestellt hat, welches Zeit Beispiel am besten ist, wird die lokale Taktfrequenz basierend auf den oben genannten Kriterien angepasst, um die konvergiert zur richtigen Zeit zuzulassen. Wenn der Zeitunterschied zwischen der lokalen Uhr und dem ausgewählten Beispiel für eine genaue Zeit (auch als Zeit Abweichung bezeichnet) zu groß ist, um durch die Anpassung der lokalen Taktrate korrigiert zu werden, legt der Zeit Dienst die Ortszeit auf die richtige Zeit fest. Diese Anpassung der Uhrzeitangabe oder der Änderung an direkter Uhrzeit wird als Takt Disziplin bezeichnet.  
  
## <a name="windows-time-service-architecture"></a>Windows-Zeitdienst-Architektur  
Der Windows-Zeit Dienst besteht aus den folgenden Komponenten:  
  
-   Dienststeuerungs-Manager  
  
-   Windows-Zeit Service Manager  
  
-   Takt Disziplin  
  
-   Zeit Anbieter  
  
Die folgende Abbildung zeigt die Architektur des Windows-Zeit Dienstanbieter.  
  
**Windows-Zeit Dienst Architektur**  
  
![Windows-Zeitdienst](../media/Windows-Time-Service/How-the-Windows-Time-Service-Works/trnt_sec_arcc.gif)
  
Der Dienststeuerungs-Manager ist dafür verantwortlich, den Windows-Zeit Dienst zu starten und zu beenden. Der Windows-Zeit Service Manager ist für das Initiieren der Aktion der im Betriebssystem enthaltenen NTP-Zeit Anbieter verantwortlich. Mit dem Windows-Zeit Service Manager werden alle Funktionen des Windows-Zeit diensdienstanbieter und die zusammen Fügung aller Zeit Beispiele gesteuert. Zusätzlich zur Bereitstellung von Informationen über den aktuellen Systemstatus, wie z. b. die aktuelle Uhrzeit Quelle oder das Zeitpunkt der letzten Aktualisierung der Systemuhr, ist die Windows-Zeit Service Manager auch für das Erstellen von Ereignissen im Ereignisprotokoll verantwortlich.  
  
Die Zeitsynchronisierung umfasst die folgenden Schritte:  
  
-   Eingabe Anbieter fordern Zeit Beispiele aus konfigurierten NTP-Zeitquellen an und empfangen Sie.  
  
-   Diese Zeit Beispiele werden dann an das Windows-Zeit Service Manager, das alle Beispiele sammelt und an die Unterkomponente der Clock-Disziplin übergibt.  
  
-   Die Unterkomponente der Clock-Disziplin wendet die NTP-Algorithmen an, die zur Auswahl des optimalen Zeit Beispiels führen.  
  
-   Die Unterkomponente der Clock-Disziplin passt die Uhrzeit der Systemuhr an die präzisere Zeit an, indem Sie entweder die Taktrate anpasst oder die Uhrzeit direkt ändert.  
  
Wenn ein Computer als Zeitserver festgelegt wurde, kann er die Zeit auf einem beliebigen Computer senden, der die Zeitsynchronisierung an einem beliebigen Punkt in diesem Vorgang anfordert.  
  
## <a name="windows-time-service-time-protocols"></a>Windows-Zeit Dienstnutzungsdauer Protokolle  

Mit Zeit Protokollen wird festgelegt, wie genau die Uhren von zwei Computern synchronisiert werden. Ein Zeitprotokoll ist dafür verantwortlich, die am besten verfügbaren Zeit Informationen zu ermitteln und die Uhren zu konvergieren, um sicherzustellen, dass eine konsistente Zeit auf separaten Systemen beibehalten wird.  
  
Der Windows-Zeit Dienst verwendet das Netzwerk Zeitprotokoll (NTP), um die Zeit über ein Netzwerk zu synchronisieren. NTP ist ein Internet Zeitprotokoll, das die für die Synchronisierung von Uhren erforderlichen Disziplin Algorithmen umfasst. NTP ist ein genaueres Zeitprotokoll als das Simple Network Time Protocol (SNTP), das in einigen Versionen von Windows verwendet wird. W32Time unterstützt jedoch weiterhin SNTP, um die Abwärtskompatibilität mit Computern zu ermöglichen, auf denen SNTP-basierte Zeit Dienste wie z. b. Windows 2000 ausgeführt werden.  
  
### <a name="network-time-protocol"></a>Netzwerk Zeitprotokoll  
Das Netzwerk Zeitprotokoll (NTP) ist das standardmäßige Zeit Synchronisierungs Protokoll, das vom Windows-Zeit Dienst im Betriebssystem verwendet wird. NTP ist ein fehlertolerantes, hochgradig skalierbares Zeitprotokoll und ist das Protokoll, das am häufigsten für die Synchronisierung von Computeruhren mithilfe eines bestimmten Zeit Verweises verwendet wird.  
  
Die NTP-Zeitsynchronisierung erfolgt über einen bestimmten Zeitraum und umfasst die Übertragung von NTP-Paketen über ein Netzwerk. NTP-Pakete enthalten Zeitstempel, die ein Zeit Beispiel sowohl vom Client als auch vom Server enthalten, die an der Zeitsynchronisierung teilnehmen.  
  
NTP verwendet eine Referenzuhr zum Definieren der genauesten Zeit, die verwendet werden soll, und synchronisiert alle Uhren eines Netzwerks mit dieser verweisuhr. NTP verwendet die koordinierte Weltzeit (UTC) als universellen Standard für die aktuelle Zeit. Die UTC ist unabhängig von Zeitzonen und ermöglicht, dass NTP unabhängig von den Zeitzoneneinstellungen überall auf der Welt verwendet werden kann.  
  
#### <a name="ntp-algorithms"></a>NTP-Algorithmen  
NTP umfasst zwei Algorithmen, einen Algorithmus zum Filtern von uhrfiltern und einen Takt Auswahl Algorithmus, um dem Windows-Zeit Dienst bei der Ermittlung des optimalen Zeit Beispiels zu helfen. Der Algorithmus für die Zeit Filterung ist für das Durchsuchen von Zeit Beispielen konzipiert, die von abgefragten Zeitquellen empfangen werden, und um die besten Zeit Beispiele aus den einzelnen Quellen zu ermitteln. Der Algorithmus für die Takt Auswahl bestimmt dann den genauesten Zeitserver im Netzwerk. Diese Informationen werden dann an den Algorithmus für die Zeit Disziplin weitergeleitet, der die gesammelten Informationen verwendet, um die lokale Uhr des Computers zu korrigieren, während gleichzeitig Fehler aufgrund der Netzwerk Latenz und der nicht Genauigkeit der Computeruhr kompensiert werden.  
  
Die NTP-Algorithmen sind bei leichten Netzwerk-und Server Ladevorgängen am genauesten. Wie bei jedem Algorithmus, der die Netzwerk Transitzeit berücksichtigt, können NTP-Algorithmen unter den Bedingungen der extrem Überlastung des Netzwerks eine schlechte Leistung bringen. Weitere Informationen zu den NTP-Algorithmen finden Sie unter RFC 1305 in der IETF RFC-Datenbank.  
  
#### <a name="ntp-time-provider"></a>NTP-Zeit Anbieter  
Der Windows-Zeit Dienst ist ein umfassendes Zeit Synchronisierungs Paket, das eine Vielzahl von Hardware Geräten und Zeit Protokollen unterstützen kann. Um diese Unterstützung zu aktivieren, verwendet der Dienst austauschbare Zeit Anbieter. Ein Zeit Anbieter ist dafür verantwortlich, entweder genaue Zeitstempel (aus dem Netzwerk oder von der Hardware) zu erhalten oder diese Zeitstempel anderen Computern über das Netzwerk bereitzustellen.  
  
Der NTP-Anbieter ist der Standardzeit Anbieter, der im Betriebssystem enthalten ist. Der NTP-Anbieter befolgt die von NTP Version 3 für einen Client und einen Server angegebenen Standards und kann mit SNTP-Clients und-Servern interagieren, um die Abwärtskompatibilität mit Windows 2000 und anderen SNTP-Clients zu Gewähr alten. Der NTP-Anbieter im Windows-Zeit Dienst besteht aus den folgenden zwei Teilen:  
  
-   **Der NtpServer-Ausgabe Anbieter.** Dabei handelt es sich um einen Zeitserver, der auf Client Zeitanforderungen im Netzwerk antwortet.  
  
-   **NtpClient-Eingabe Anbieter.** Dabei handelt es sich um einen Zeit Client, der Zeit Informationen aus einer anderen Quelle (einem Hardware Gerät oder einem NTP-Server) abruft und Zeit Beispiele zurückgeben kann, die für die Synchronisierung der lokalen Uhr nützlich sind.  
  
Obwohl die tatsächlichen Vorgänge dieser beiden Anbieter eng miteinander verknüpft sind, werden Sie unabhängig vom Zeit Dienst angezeigt. Ab Windows 2000 Server wird ein Windows-Computer, auf dem ein Windows-Computer mit einem Netzwerk verbunden ist, als NTP-Client konfiguriert. Außerdem versuchen Computer, auf denen der Windows-Zeit Dienst ausgeführt wird, nur die Zeit mit einem Domänen Controller oder einer manuell angegebenen Zeit Quelle zu synchronisieren. Dies sind die bevorzugten Zeit Anbieter, da Sie automatisch verfügbar und sichere Zeitquellen sind.  
  
#### <a name="ntp-security"></a>NTP-Sicherheit  

Innerhalb einer AD DS-Gesamtstruktur basiert der Windows-Zeit Dienst auf Sicherheitsfeatures der Standard Domäne, um die Authentifizierung von Zeit Daten zu erzwingen. Die Sicherheit von NTP-Paketen, die zwischen einem Domänen Mitglieds Computer und einem lokalen Domänen Controller gesendet werden, der als Zeitserver fungiert, basiert auf der Authentifizierung mit gemeinsam verwendetem Schlüssel. Der Windows-Zeit Dienst verwendet den Kerberos-Sitzungsschlüssel des Computers, um authentifizierte Signaturen für NTP-Pakete zu erstellen, die über das Netzwerk gesendet werden. NTP-Pakete werden nicht innerhalb des sicheren Kanals für die Netzwerk Anmeldung übertragen. Wenn ein Computer die Zeit von einem Domänen Controller in der Domänen Hierarchie anfordert, erfordert der Windows-Zeit Dienst stattdessen, dass die Uhrzeit authentifiziert wird. Der Domänen Controller gibt dann die erforderlichen Informationen in Form eines 64-Bit-Werts zurück, der mit dem Sitzungsschlüssel aus dem Anmeldedienst authentifiziert wurde. Wenn das zurückgegebene NTP-Paket nicht mit dem Sitzungsschlüssel des Computers signiert oder falsch signiert wurde, wird die Zeit abgelehnt. Alle Authentifizierungsfehler werden im Ereignisprotokoll protokolliert. Auf diese Weise stellt der Windows-Zeit Dienst Sicherheit für NTP-Daten in einer AD DS Gesamtstruktur bereit.  
  
Im Allgemeinen erhalten Windows-Zeit Clients automatisch eine genaue Zeit für die Synchronisierung von Domänen Controllern in derselben Domäne. In einer Gesamtstruktur wird von den Domänen Controllern einer untergeordneten Domäne Zeit mit Domänen Controllern in ihren übergeordneten Domänen synchronisiert. Wenn ein Zeitserver ein authentifiziertes NTP-Paket an einen Client zurückgibt, der die Zeit anfordert, wird das Paket mithilfe eines Kerberos-Sitzungsschlüssels signiert, der durch ein vertrauenswürdiges Konto für die Domänen Domäne definiert ist. Das Konto für die Vertrauenswürdigkeit der vertrauenswürdigen Domäne wird erstellt, wenn eine neue AD DS Domäne einer Gesamtstruktur Beitritt und der Anmeldedienst den Sitzungsschlüssel verwaltet. Auf diese Weise wird der als zuverlässig konfigurierte Domänen Controller in der Stamm Domäne der Gesamtstruktur zur authentifizierten Zeit Quelle für alle Domänen Controller in den übergeordneten und untergeordneten Domänen und indirekt für alle Computer in der Domänen Struktur.  
  
Der Windows-Zeit Dienst kann für die Zusammenarbeit zwischen Gesamtstrukturen konfiguriert werden. es ist jedoch wichtig zu beachten, dass diese Konfiguration nicht sicher ist. Beispielsweise kann ein NTP-Server in einer anderen Gesamtstruktur verfügbar sein. Da sich dieser Computer jedoch in einer anderen Gesamtstruktur befindet, gibt es keinen Kerberos-Sitzungsschlüssel, mit dem NTP-Pakete signiert und authentifiziert werden können. Zum Abrufen der exakten Zeitsynchronisierung von einem Computer in einer anderen Gesamtstruktur benötigt der Client Netzwerk Zugriff auf diesen Computer, und der Zeit Dienst muss für die Verwendung einer bestimmten Zeit Quelle in der anderen Gesamtstruktur konfiguriert werden. Wenn ein Client manuell so konfiguriert ist, dass er von einem NTP-Server außerhalb der eigenen Domänen Hierarchie auf Zeit zugreift, werden die zwischen dem Client und dem Zeitserver gesendeten NTP-Pakete nicht authentifiziert und sind daher nicht sicher. Selbst bei der Implementierung von Gesamtstruktur-Vertrauens Stellungen ist der Windows-Zeit Dienst nicht in Gesamtstrukturen sicher. Obwohl der sichere Kanal für die Netzwerk Anmeldung der Authentifizierungsmechanismus für den Windows-Zeit Dienst ist, wird die Gesamtstruktur übergreifende Authentifizierung nicht unterstützt.  
  
#### <a name="hardware-devices-that-are-supported-by-the-windows-time-service"></a>Hardware Geräte, die vom Windows-Zeit Dienst unterstützt werden  
Hardware basierte Uhren, z. b. GPS oder Radio Uhren, werden häufig als äußerst genaue Referenz Takt Geräte verwendet. Standardmäßig unterstützt der NTP-Zeit Anbieter für den Windows-Zeit Dienst keine direkte Verbindung eines Hardware Geräts mit einem Computer, obwohl es möglich ist, einen softwarebasierten unabhängigen Zeit Anbieter zu erstellen, der diesen Verbindungstyp unterstützt. Diese Art von Anbieter kann in Verbindung mit dem Windows-Zeit Dienst einen zuverlässigen, stabilen Zeit Verweis bereitstellen.  
  
Hardware Geräte, z. b. eine Cesium-Uhr oder ein GPS-Empfänger (GPS), bieten eine genaue aktuelle Zeit, indem Sie einem Standard folgen, um eine genaue Zeitdefinition zu erhalten. Cesium-Uhren sind äußerst stabil und sind von Faktoren wie Temperatur, Druck oder Luftfeuchtigkeit nicht betroffen, sind aber auch sehr aufwendig. Der Betrieb eines GPS-Empfängers ist viel günstiger und auch eine exakte verweisuhr. GPS-Empfänger erhalten Ihre Zeit von Satelliten, die Ihre Zeit von einer Cesium-Uhr erhalten. Ohne die Verwendung eines unabhängigen Zeit Anbieters können Windows-Zeitserver Ihre Zeit abrufen, indem Sie eine Verbindung mit einem externen NTP-Server herstellen, der über ein Telefon oder das Internet mit einem Hardware Gerät verbunden ist. Organisationen wie das USA Naval-Observatorium stellen NTP-Server bereit, die mit äußerst zuverlässigen Referenzuhren verbunden sind.  
  
Viele GPS-Empfänger und andere Geräte können als NTP-Server in einem Netzwerk fungieren. Sie können die AD DS-Gesamtstruktur so konfigurieren, dass die Zeit von diesen externen Hardware Geräten nur synchronisiert wird, wenn Sie auch als NTP-Server in Ihrem Netzwerk fungieren. Konfigurieren Sie hierzu den Domänen Controller, der als primärer Domänen Controller-Emulator (PDC) in Ihrem Gesamtstruktur Stamm fungiert, um die Synchronisierung mit dem NTP-Server durchzuführen, der über das GPS-Gerät Informationen hierzu finden Sie unter [Konfigurieren des Windows-Zeit Diensts für den PDC-Emulator in der Stamm Domäne der](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29)Gesamtstruktur.  
  
### <a name="simple-network-time-protocol"></a>Einfaches Netzwerk Zeitprotokoll  
Das Simple Network Time Protocol (SNTP) ist ein vereinfachtes Zeitprotokoll, das für Server und Clients vorgesehen ist, die den von NTP bereitgestellten Genauigkeits Grad nicht benötigen. SNTP, eine rudimentäre Version von NTP, ist das primäre Zeitprotokoll, das in Windows 2000 verwendet wird. Da die Netzwerk Paketformate SNTP und NTP identisch sind, sind die beiden Protokolle interoperabel. Der Hauptunterschied zwischen den beiden besteht darin, dass SNTP nicht über die Fehler Verwaltung und komplexe Filtersysteme verfügt, die NTP bereitstellt. Weitere Informationen zum Protokoll für die einfache Netzwerk Zeit finden Sie unter RFC 1769 in der IETF RFC-Datenbank.  
  
### <a name="time-protocol-interoperability"></a>Interoperabilität des Zeit Protokolls  
Der Windows-Zeit Dienst kann in einer gemischten Umgebung mit Computern unter Windows 2000, Windows XP und Windows Server 2003 ausgeführt werden, da das in Windows 2000 verwendete SNTP-Protokoll mit dem NTP-Protokoll in Windows XP und Windows Server 2003 interoperabel ist.  
  
Der Zeit Dienst in Windows NT Server 4,0 mit dem Namen TimeServ synchronisiert die Zeit in einem Windows NT 4,0-Netzwerk. TimeServ ist ein Add-on-Feature, das als Teil des *Microsoft Windows NT 4,0 Resource Kits* verfügbar ist und nicht den Grad an Zuverlässigkeit der Zeitsynchronisierung bietet, der von Windows Server 2003 benötigt wird.  
  
Der Windows-Zeit Dienst kann mit Computern interagieren, auf denen Windows NT 4,0 ausgeführt wird, da die Zeit mit Computern mit Windows 2000 oder Windows Server 2003 synchronisiert werden kann. auf einem Computer mit Windows 2000 oder Windows Server 2003 werden Windows NT 4,0-Zeitserver jedoch nicht automatisch erkannt. Wenn Ihre Domäne z. b. so konfiguriert ist, dass die Zeit mithilfe der Hierarchie basierten Synchronisierungsmethode der Domäne synchronisiert wird, und Sie möchten, dass Computer in der Domänen Hierarchie die Zeit mit einem Windows NT 4,0-Domänen Controller synchronisieren, müssen Sie diese konfigurieren. Manuelles Synchronisieren von Computern mit den Windows NT 4,0-Domänen Controllern.  
  
Windows NT 4,0 verwendet einen einfacheren Mechanismus für die Zeitsynchronisierung, als der Windows-Zeit Dienst verwendet. Um eine genaue Zeitsynchronisierung über das Netzwerk sicherzustellen, empfiehlt es sich daher, alle Windows NT 4,0-Domänen Controller auf Windows 2000 oder Windows Server 2003 zu aktualisieren.  
  
## <a name="windows-time-service-processes-and-interactions"></a>Windows-Zeit Dienst Prozesse und-Interaktionen  

Der Windows-Zeit Dienst ist so konzipiert, dass die Uhren von Computern in einem Netzwerk synchronisiert werden. Der Synchronisierungs Prozess für die Netzwerk Zeit (auch Zeit Konvergenz genannt) tritt im gesamten Netzwerk auf, da jeder Computer von einem präziseren Zeitserver aus auf die Zeit zugreift. Die Zeit Konvergenz umfasst einen Prozess, durch den ein autoritativer Server den aktuellen Zeitpunkt der Client Computer in Form von NTP-Paketen bereitstellt. Die in einem Paket enthaltenen Informationen geben an, ob eine Anpassung an der aktuellen Uhrzeit des Computers vorgenommen werden muss, damit Sie mit dem genaueren Server synchronisiert wird.  
  
Im Rahmen des Zeit Konvergenz Vorgangs versuchen Domänen Mitglieder, die Zeit mit einem beliebigen Domänen Controller in derselben Domäne zu synchronisieren. Wenn der Computer ein Domänen Controller ist, wird versucht, eine Synchronisierung mit einem autorisierteren Domänen Controller durchzusetzen.  
  
Computer, auf denen Windows XP Home Edition ausgeführt wird, oder Computer, die keiner Domäne beigetreten sind, versuchen nicht, eine Synchronisierung mit der Domänen Hierarchie durchzuführen. Sie werden jedoch standardmäßig konfiguriert, um Zeit von Time.Windows.com  
  
Zum Einrichten eines Computers, auf dem Windows Server 2003 als autorisierend ausgeführt wird, muss der Computer als zuverlässige Zeit Quelle konfiguriert werden. Standardmäßig wird der erste Domänen Controller, der auf einer Windows Server 2003-Domäne installiert ist, automatisch als zuverlässige Zeit Quelle konfiguriert. Da es sich um den autorisierenden Computer für die Domäne handelt, muss er so konfiguriert werden, dass er mit einer externen Zeit Quelle und nicht mit der Domänen Hierarchie synchronisiert wird. Standardmäßig sind alle anderen Domänen Mitglieder von Windows Server 2003 so konfiguriert, dass Sie mit der Domänen Hierarchie synchronisiert werden.  
  
Nachdem Sie ein Windows Server 2003-Netzwerk eingerichtet haben, können Sie den Windows-Zeit Dienst so konfigurieren, dass eine der folgenden Optionen für die Synchronisierung verwendet wird:  
  
-   Synchronisierung auf Domänen Hierarchie  
  
-   Eine manuell angegebene Synchronisierungs Quelle  
  
-   Alle verfügbaren Synchronisierungs Mechanismen  
  
-   Keine Synchronisierung.  
  
Diese Synchronisierungs Typen werden im folgenden Abschnitt erläutert.  
  
### <a name="domain-hierarchy-based-synchronization"></a>Synchronisierung auf Domänen Hierarchie  

Bei der Synchronisierung, die auf einer Domänen Hierarchie basiert, wird in der AD DS Domänen Hierarchie eine zuverlässige Quelle gefunden, mit der die Zeit synchronisiert werden Basierend auf der Domänen Hierarchie bestimmt der Windows-Zeit Dienst die Genauigkeit jedes Zeit Servers. In einer Windows Server 2003-Gesamtstruktur enthält der Computer, der die Betriebs Master Rolle des primären Domänen Controllers (PDC) in der Stamm Domäne der Gesamtstruktur enthält, die Position der besten Zeit Quelle, es sei denn, es wurde eine andere zuverlässige Zeit Quelle konfiguriert. In der folgenden Abbildung wird ein Pfad zur Zeitsynchronisierung zwischen Computern in einer Domänen Hierarchie veranschaulicht.  
  
**Zeitsynchronisierung in einer AD DS Hierarchie**  
![Windows-Zeit](../media/Windows-Time-Service/How-the-Windows-Time-Service-Works/trnt_ntw_adhc.gif)
  
#### <a name="reliable-time-source-configuration"></a>Zuverlässige Zeit Quell Konfiguration  
Ein Computer, der als zuverlässige Zeit Quelle konfiguriert ist, wird als Stamm des Zeit dienstanzdienstanzen identifiziert. Der Stamm des Zeit dienstanzdienstanzen ist der autorisierende Server für die Domäne und wird in der Regel so konfiguriert, dass er von einem externen NTP-Server oder einem Hardware Gerät Zeit Ein Zeitserver kann als zuverlässige Zeit Quelle konfiguriert werden, um zu optimieren, wie die Zeit in der gesamten Domänen Hierarchie übertragen wird. Wenn ein Domänen Controller als zuverlässige Zeit Quelle konfiguriert ist, kündigt der Anmeldedienst den Domänen Controller als zuverlässige Zeit Quelle an, wenn er sich am Netzwerk anmeldet. Wenn andere Domänen Controller nach einer Zeit Quelle suchen, mit der synchronisiert werden soll, wählen Sie zuerst eine zuverlässige Quelle aus, sofern eine verfügbar ist.  
  
#### <a name="time-source-selection"></a>Zeitquellen Auswahl  
Der Vorgang zur Auswahl der Zeit Quelle kann zwei Probleme in einem Netzwerk verursachen:  
  
-   Zusätzliche Synchronisierungs Zyklen.  
  
-   Höheres Volumen im Netzwerk Datenverkehr.  
  
Eine Verbindung im Synchronisierungs Netzwerk tritt auf, wenn die Zeit zwischen einer Gruppe von Domänen Controllern konstant bleibt und die gleiche Zeit fortlaufend ohne eine erneute Synchronisierung mit einer anderen zuverlässigen Zeit Quelle gemeinsam genutzt wird. Der Zeitquellen Auswahl-Algorithmus des Windows Time Service ist für den Schutz vor diesen Arten von Problemen konzipiert.  
  
Ein Computer verwendet eine der folgenden Methoden, um eine Zeit Quelle für die Synchronisierung zu identifizieren:  
  
-   Wenn der Computer kein Mitglied einer Domäne ist, muss er so konfiguriert werden, dass er eine Synchronisierung mit einer bestimmten Zeit Quelle durchläuft.  
  
-   Wenn der Computer ein Mitglieds Server oder eine Arbeitsstation in einer Domäne ist, wird er standardmäßig der AD DS Hierarchie folgen und seine Zeit mit einem Domänen Controller in der lokalen Domäne synchronisieren, auf der derzeit der Windows-Zeit Dienst ausgeführt wird.  
  
Wenn es sich bei dem Computer um einen Domänen Controller handelt, sind bis zu sechs Abfragen zum Auffinden eines anderen Domänen Controllers für die Synchronisierung möglich. Jede Abfrage ist so konzipiert, dass Sie eine Zeit Quelle mit bestimmten Attributen identifiziert, z. b. eine Art von Domänen Controller, eine bestimmte Position und ob es sich um eine zuverlässige Zeit Quelle handelt. Die Zeit Quelle muss außerdem die folgenden Einschränkungen einhalten:  
  
-   Eine zuverlässige Zeit Quelle kann nur mit einem Domänen Controller in der übergeordneten Domäne synchronisiert werden.  
  
-   Ein PDC-Emulator kann mit einer zuverlässigen Zeit Quelle in der eigenen Domäne oder einem beliebigen Domänen Controller in der übergeordneten Domäne synchronisiert werden.  
  
Wenn der Domänen Controller nicht mit dem Typ des Domänen Controllers synchronisiert werden kann, der abgefragt wird, wird die Abfrage nicht durchgeführt. Der Domänen Controller weiß, von welchem Computertyp er Zeit abrufen kann, bevor er die Abfrage ausführt. Beispielsweise versucht ein lokaler PDC-Emulator nicht, die drei oder sechs Ziffern abzufragen, weil ein Domänen Controller nicht versucht, eine Synchronisierung mit sich selbst durchzuführen.  
  
In der folgenden Tabelle sind die Abfragen aufgelistet, die von einem Domänen Controller vorgenommen werden, um eine Zeit Quelle und die Reihenfolge der Abfragen zu finden.  
  
**Domänen Controller-Zeit Quell Abfragen**  
  
|Abfrage Nummer|Domänencontroller|Speicherort|Zuverlässigkeit der Zeit Quelle|  
|----------------|---------------------|------------|------------------------------|  
|1|Übergeordneter Domänen Controller|In-Site|Bevorzugt eine zuverlässige Zeit Quelle, kann jedoch mit einer nicht zuverlässigen Zeit Quelle synchronisiert werden, wenn alles verfügbar ist.|  
|2|Lokaler Domänen Controller|In-Site|Wird nur mit einer zuverlässigen Zeit Quelle synchronisiert.|  
|3|Lokaler PDC-Emulator|In-Site|Gilt nicht.<br /><br />Ein Domänen Controller versucht nicht, eine Synchronisierung mit sich selbst durchführen.|  
|4|Übergeordneter Domänen Controller|Außerhalb des Standorts|Bevorzugt eine zuverlässige Zeit Quelle, kann jedoch mit einer nicht zuverlässigen Zeit Quelle synchronisiert werden, wenn alles verfügbar ist.|  
|5|Lokaler Domänen Controller|Außerhalb des Standorts|Wird nur mit einer zuverlässigen Zeit Quelle synchronisiert.|  
|6|Lokaler PDC-Emulator|Außerhalb des Standorts|Gilt nicht.<br /><br />Ein Domänen Controller versucht nicht, eine Synchronisierung mit sich selbst durchführen.| 
  
**Hinweis**  
  
-   Ein Computer wird nie mit sich selbst synchronisiert. Wenn der Computer, der die Synchronisierung versucht, der lokale PDC-Emulator ist, versucht er nicht, die Abfragen 3 oder 6 durchführen  
  
Jede Abfrage gibt eine Liste von Domänen Controllern zurück, die als Zeit Quelle verwendet werden können. Windows-Zeit weist jedem Domänen Controller, der eine Bewertung abgefragt, basierend auf der Zuverlässigkeit und dem Speicherort des Domänen Controllers zu. In der folgenden Tabelle werden die von der Windows-Zeit für die einzelnen Domänen Controller zugewiesenen Bewertungen aufgeführt.  
  
**Bewertung ermitteln**  
  
|Status des Domänen Controllers|Wert|  
|----------------------------|---------|  
|Domänen Controller am selben Standort|8|  
|Als zuverlässige Zeit Quelle gekennzeichneter Domänen Controller|4|  
|Domänen Controller in der übergeordneten Domäne|2|  
|Domänen Controller, der ein PDC-Emulator ist|1|  
  
Wenn der Windows-Zeit Dienst feststellt, dass er den Domänen Controller mit der bestmöglichen Bewertung identifiziert hat, werden keine weiteren Abfragen durchgeführt. Die vom Zeit Dienst zugewiesenen Ergebnisse sind kumulativ. Dies bedeutet, dass ein PDC-Emulator, der sich an demselben Standort befindet, eine Bewertung von neun erhält.  
  
Wenn der Stamm des Zeit Dienes nicht für die Synchronisierung mit einer externen Quelle konfiguriert ist, steuert die interne Hardwareuhr des Computers die Zeit.  
  
### <a name="manually-specified-synchronization"></a>Manuell angegebene Synchronisierung  
Mithilfe der manuell angegebenen Synchronisierung können Sie einen einzelnen Peer oder eine Liste von Peers festlegen, von denen ein Computerzeit erhält. Wenn der Computer kein Mitglied einer Domäne ist, muss er manuell so konfiguriert werden, dass er eine Synchronisierung mit einer bestimmten Zeit Quelle durchläuft. Ein Computer, der Mitglied einer Domäne ist, wird standardmäßig für die Synchronisierung über die Domänen Hierarchie konfiguriert. die manuell angegebene Synchronisierung ist besonders nützlich für den Gesamtstruktur Stamm der Domäne oder für Computer, die keiner Domäne angehören. Manuelles angeben eines externen NTP-Servers für die Synchronisierung mit dem autorisierenden Computer für Ihre Domäne sorgt für zuverlässige Zeit. Das Konfigurieren des autorisierenden Computers für Ihre Domäne für die Synchronisierung mit einer Hardwareuhr ist jedoch eine bessere Lösung für die Bereitstellung der genauesten und sichersten Zeit für Ihre Domäne.  
  
Manuell angegebene Zeitquellen werden nicht authentifiziert, es sei denn, ein bestimmter Zeit Anbieter wird für Sie geschrieben, und Sie sind daher für Angreifer anfällig. Wenn ein Computer mit einer manuell angegebenen Quelle anstelle seines authentifizier enden Domänen Controllers synchronisiert wird, sind die beiden Computer möglicherweise nicht mehr synchronisiert, sodass die Kerberos-Authentifizierung fehlschlägt. Dies kann dazu führen, dass andere Aktionen, die die Netzwerk Authentifizierung erfordern, fehlschlagen, wie z. b Wenn nur der Gesamtstruktur Stamm für die Synchronisierung mit einer externen Quelle konfiguriert ist, bleiben alle anderen Computer innerhalb der Gesamtstruktur miteinander synchronisiert, sodass Wiedergabe Angriffe schwierig werden.  
  
### <a name="all-available-synchronization-mechanisms"></a>Alle verfügbaren Synchronisierungs Mechanismen  

Die Option "alle verfügbaren Synchronisierungs Mechanismen" ist die wertvollsten Synchronisierungsmethode für Benutzer in einem Netzwerk. Diese Methode ermöglicht die Synchronisierung mit der Domänen Hierarchie und bietet möglicherweise auch eine Alternative Zeit Quelle, wenn die Domänen Hierarchie in Abhängigkeit von der Konfiguration nicht verfügbar ist. Wenn der Client die Zeit mit der Domänen Hierarchie nicht synchronisieren kann, greift die Zeit Quelle automatisch auf die durch die **NtpServer** -Einstellung angegebene Zeit Quelle zurück. Diese Synchronisierungsmethode bietet höchstwahrscheinlich eine genaue Zeit für Clients.  

### <a name="stopping-time-synchronization"></a>Beenden der Zeitsynchronisierung  
Es gibt bestimmte Situationen, in denen Sie verhindern möchten, dass ein Computer seine Zeit synchronisiert. Wenn ein Computer z. b. versucht, eine Synchronisierung von einer Zeit Quelle im Internet oder von einem anderen Standort über ein WAN über eine DFÜ-Verbindung durchzusetzen, kann dies kostspielige Telefongebühren verursachen. Wenn Sie die Synchronisierung auf diesem Computer deaktivieren, verhindern Sie, dass der Computer über eine DFÜ-Verbindung auf eine Zeit Quelle zugreift.  
  
Sie können die Synchronisierung auch deaktivieren, um die Generierung von Fehlern im Ereignisprotokoll zu verhindern. Jedes Mal, wenn ein Computer versucht, eine Synchronisierung mit einer nicht verfügbaren Zeit Quelle durchzusetzen, generiert er einen Fehler im Ereignisprotokoll. Wenn eine Zeit Quelle für eine geplante Wartung aus dem Netzwerk entfernt wird und Sie nicht beabsichtigen, den Client so zu konfigurieren, dass er von einer anderen Quelle aus synchronisiert wird, können Sie die Synchronisierung auf dem Client deaktivieren, um zu verhindern, dass die Synchronisierung während des Zeit Servers erfolgt. ist nicht verfügbar.  
  
Es ist hilfreich, die Synchronisierung auf dem Computer zu deaktivieren, der als Stammverzeichnis des Synchronisierungs Netzwerks festgelegt ist. Dies gibt an, dass der Stamm Computer der lokalen Uhr vertraut. Wenn das Stammverzeichnis der Synchronisierungs Hierarchie nicht auf **nosync** festgelegt ist und die Synchronisierung mit einer anderen Zeit Quelle nicht möglich ist, akzeptieren Clients das Paket nicht, das von diesem Computer gesendet wird, weil die Zeit nicht vertrauenswürdig ist.
  
Die einzigen Zeitserver, die von Clients als vertrauenswürdig eingestuft werden, selbst wenn Sie nicht mit einer anderen Zeit Quelle synchronisiert wurden, sind solche, die vom Client als zuverlässige Zeitserver identifiziert wurden.  
  
### <a name="disabling-the-windows-time-service"></a>Der Windows-Zeit Dienst wird deaktiviert.  
Der Windows-Zeit Dienst (W32Time) kann vollständig deaktiviert werden. Wenn Sie ein Produkt für die Zeitsynchronisierung von Drittanbietern implementieren möchten, das NTP verwendet, müssen Sie den Windows-Zeit Dienst deaktivieren. Der Grund hierfür ist, dass alle NTP-Server auf UDP-Port 123 (User Datagram Protocol) zugreifen müssen, und solange der Windows-Zeit Dienst unter dem Betriebssystem Windows Server 2003 ausgeführt wird, bleibt Port 123 für die Windows-Zeit reserviert.  
  
## <a name="network-ports-used-by-windows-time-service"></a>Vom Windows-Zeit Dienst verwendete Netzwerkports  
Der Windows-Zeit Dienst kommuniziert in einem Netzwerk, um zuverlässige Zeitquellen zu ermitteln, Zeit Informationen zu erhalten und anderen Computern Zeit Informationen bereitzustellen. Diese Kommunikation wird durch die RFCs NTP und SNTP definiert.  
  
**Port Zuweisungen für den Windows-Zeit Dienst**  
  
|Dienstname|UDP|TCP|  
|----------------|-------|-------|  
|NTP|123|N/V|  
|SNTP|123|N/V|  
  
## <a name="see-also"></a>Weitere Informationen  
[Technische Referenz für den Windows-Zeit Dienst](windows-time-service-tech-ref.md)
[Windows-Zeit Dienst Tools und-Einstellungen](Windows-Time-Service-Tools-and-Settings.md)
[Microsoft Knowledge Base-Artikel 902229](https://go.microsoft.com/fwlink/?LinkId=186066)