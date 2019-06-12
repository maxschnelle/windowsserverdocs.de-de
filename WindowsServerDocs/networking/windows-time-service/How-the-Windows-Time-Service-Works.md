---
ms.assetid: d1953097-63ea-4a0e-b860-2f3b7c175c41
title: Funktionsweise des Windows-Zeitdiensts
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 9e4131c28a18a50f3312e5e0201a0ed9529d4555
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812397"
---
# <a name="how-the-windows-time-service-works"></a>Funktionsweise des Windows-Zeitdiensts

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

**In diesem Abschnitt**  
  
-   [Windows-Zeitdienst-Architektur](#windows-time-service-architecture)  
  
-   [Windows Time Service Time-Protokolle](#windows-time-service-time-protocols)  
  
-   [Windows Time Serviceprozesse und-Interaktionen](#windows-time-service-processes-and-interactions)  
  
-   [Von Windows-Zeitdienst verwendete Netzwerkports](#network-ports-used-by-windows-time-service)  
  
> [!NOTE]  
> In diesem Thema wird erläutert, wie nur die Windows-Zeitdienst (W32Time) funktioniert. Informationen zum Konfigurieren der Windows-Zeitdienst, finden Sie unter [Konfigurieren von Systemen für hohe Genauigkeit](configuring-systems-for-high-accuracy.md).
  
> [!NOTE]  
> In Windows Server 2003 und Microsoft Windows 2000 Server heißt der Verzeichnisdienst Active Directory-Dienst. In Windows Server 2008 und höheren Versionen heißt der Verzeichnisdienst Active Directory Domain Services (AD DS). Im weiteren Verlauf dieses Themas wird Bezug auf AD DS genommen, die Informationen gelten jedoch auch für Active Directory.  
  
Obwohl der Windows-Zeitdienst nicht um eine genaue Implementierung des Network Time Protocol (NTP) ist, wird die komplexe Sammlung von Algorithmen, die in den NTP-Spezifikationen, um sicherzustellen, dass die Uhren auf den Computern in einem Netzwerk so exakt wie möglich definiert ist. Im Idealfall werden alle Computeruhren in AD DS-Domäne mit der Zeit von einem autorisierenden Computer synchronisiert. Zeitsynchronisierung in einem Netzwerk können von vielen Faktoren beeinflusst werden. Die folgenden Faktoren beeinflussen die Genauigkeit der in AD DS-Synchronisierung:  
  
-   Die netzwerkbedingungen  
  
-   Die Genauigkeit der Hardware-Uhr des Computers  
  
-   Die Menge an CPU- und Ressourcen, die der Windows-Zeitdienst  
  
> [!IMPORTANT]  
> Vor Windows Server 2016 wurde der W32Time-Dienst nicht für zeitempfindliche Anwendung Bedürfnissen entwickelt.  Updates für Windows Server 2016 nun ermöglichen jedoch zum Implementieren einer Lösung für 1 ms Genauigkeit in Ihrer Domäne.  Finden Sie unter [Windows 2016 genau Zeit](accurate-time.md) und [Unterstützung Grenze so konfigurieren Sie den Windows-Zeitdienst für Umgebungen mit hoher Genauigkeit](support-boundary.md) für Weitere Informationen.  
  
Computer, die synchronisieren ihre Zeit weniger häufig oder sind nicht Mitglied einer Domäne, sind konfiguriert, wird standardmäßig mit time.windows.com synchronisiert.  Aus diesem Grund ist es unmöglich zu garantieren uhrzeitsynchronisierungsdienst auf Computern, die zeitweilig verfügen oder keine Netzwerkverbindungen.  
  
Eine AD DS-Gesamtstruktur verfügt über einer vorher bestimmten Zeit für Synchronisierung-Hierarchie. Der Windows-Zeitdienst wird die Zeit zwischen Computern in der Hierarchie, wobei die genauesten Verweis Uhren oben synchronisiert. Wenn mehr als eine Datenquelle für die Zeit auf einem Computer konfiguriert ist, verwendet Windows-Uhrzeit NTP-Algorithmen, die konfigurierten Datenquellen basierend auf die Fähigkeit des Computers mit dieser Zeitquelle synchronisieren die beste Zeitquelle aus. Der Windows-Zeitdienst unterstützt keine Netzwerk-Synchronisierung von Broadcast oder multicast-Peers. Weitere Informationen zu diesen NTP-Funktionen finden Sie unter RFC 1305 in der IETF RFC-Datenbank.  
  
Jeder Computer mit der Windows-Zeitdienst verwendet der Dienst die genaueste Zeit beibehalten. Computer, die Mitglied einer Domäne sind, die als Time-Client standardmäßig fungieren, daher in den meisten Fällen ist es nicht zum Konfigurieren der Windows-Zeitdienst. Allerdings der Windows-Zeitdienst kann so konfiguriert werden, dass die Zeit von einer angegebenen Zeit Verweisquelle anfordern, und können auch Zeit für Clients bereitstellen.
  
Der Grad, zu dem Zeit des Computers korrekt ist, wird eine Stratum aufgerufen. Die genaueste Zeitquelle in einem Netzwerk (z. B. eine Hardware-Format), nimmt der untersten Ebene der Stratum oder Stratum eine. Diese genauen Zeitquelle wird eine Uhr Verweis bezeichnet. Ein NTP-Server, der direkt aus einer Verweis Uhr Zeit verwendet nimmt eine Stratum, die eine Ebene höher als bei der Uhr auf der Verweis ist. Ressourcen, die aus dem NTP-Server zu erwerben sind zwei Schritte, bis die Uhr Verweis aus diesem Grund belegen eine Schicht, die zwei ist höher als die genaueste Zeitquelle und so weiter. Als eines Computers Stratum Zahl erhöht, die Zeit der Systemuhr möglicherweise weniger genau. Daher ist die Stratum auf jedem Computer ein Indikator dafür, wie genau dieser Computer mit dem die genauesten Zeitquelle synchronisiert wird.  
  
Wenn der W32Time-Manager Stichproben erhält, verwendet er spezielle Algorithmen in NTP um zu bestimmen, welche die Time-Beispiele verwenden die am besten geeignet ist. Der Zeitdienst verwendet auch einen anderen Satz von Algorithmen, um zu bestimmen, welche die konfigurierte Zeitquellen die genaueste Lösung darstellt. Wenn der Zeitdienst die Time-Beispiel am besten geeignet ist ermittelt hat, wird angepasst basierend auf den oben genannten Kriterien, die lokale Uhr Rate so, dass auf die richtige Uhrzeit konvergiert können. Wenn der Zeitunterschied zwischen lokalen Uhrzeit und das ausgewählte genaue Uhrzeit-Beispiel (so genannte Zeit skew) zu groß, um das Anpassen der Rate für die lokale Uhr ist, legt der Zeitdienst die lokale Uhr auf die richtige Uhrzeit fest. Diese Anpassung der Taktrate oder direkte Uhrzeit geändert wird als Uhr Disziplin bezeichnet.  
  
## <a name="windows-time-service-architecture"></a>Windows-Zeitdienst-Architektur  
Der Windows-Zeitdienst besteht aus folgenden Komponenten:  
  
-   Dienststeuerungs-Manager  
  
-   Windows Time Service Manager  
  
-   Disziplin der Uhr  
  
-   Time-Anbieter  
  
Die folgende Abbildung zeigt die Architektur des Windows-Zeitdiensts.  
  
**Windows-Zeitdienst-Architektur**  
  
![Windows-Zeitdienst](../media/Windows-Time-Service/How-the-Windows-Time-Service-Works/trnt_sec_arcc.gif)
  
Der Dienststeuerungs-Manager ist verantwortlich für das Starten und beenden den Windows-Zeitdienst. Die Windows Time Service Manager ist verantwortlich für das Initiieren der Aktion die NTP-Zeit-Anbieter mit dem Betriebssystem enthalten. Die Windows Time Service Manager steuert alle Funktionen der Windows-Zeitdienst und die Zusammenfügung aller Zeit Beispiele. Zusätzlich zur Bereitstellung Informationen zu den aktuellen Systemstatus, wie z. B. die aktuelle Zeitquelle oder das letzte Zeit die Systemuhr aktualisiert wurde, ist die Windows Time Service Manager auch verantwortlich für das Erstellen von Ereignissen im Ereignisprotokoll.  
  
Der Synchronisierungsvorgang für die Zeit umfasst die folgenden Schritte aus:  
  
-   Geben Sie die Anbieter-Anforderung und empfangen Sie Stichproben von konfigurierten NTP-Zeitquellen.  
  
-   Diese Zeit Beispiele werden klicken Sie dann auf Windows Time Service Manager übergeben, die alle Beispiele erfasst, und übergibt sie an die Uhr Disziplin Unterkomponente.  
  
-   Die Uhr Disziplin Unterkomponente gilt die NTP-Algorithmen die in der Auswahl des besten Zeit Beispiels führt.  
  
-   Die Uhr Disziplin Unterkomponente passt die Zeit der Systemuhr auf die genaueste Zeit durch Anpassen der Taktfrequenz oder direkt zu die Zeit ändern.  
  
Wenn ein Computer als einen Zeitserver festgelegt wurde, kann er die Zeit an einem beliebigen Computer Anfordern von Synchronisierung zu einem beliebigen Zeitpunkt in diesem Prozess senden.  
  
## <a name="windows-time-service-time-protocols"></a>Windows Time Service Time-Protokolle  

Protokolle von Zeit zu bestimmen, wie genau zwei Computern Uhren werden synchronisiert. Ein Time-Protokoll dient beim Ermitteln der beste Zeitpunkt der Verfügbarkeit der Informationen und konvergieren die Uhren, um sicherzustellen, dass es sich bei einem konsistenten Zeitpunkt auf separaten Systemen verwaltet wird.  
  
Der Windows-Zeitdienst verwendet das Network Time Protocol (NTP) um die Zeit in einem Netzwerk synchronisieren. NTP ist ein Internetprotokoll für die Zeit, die die Disziplin Algorithmen erforderlich für die Synchronisierung von Uhren enthält. NTP ist eine genauere Time-Protokoll als SNTP Simple Network Time Protocol (), die in einigen Versionen von Windows verwendet wird. W32Time SNTP zum Aktivieren der Abwärtskompatibilität mit Computern mit der Zeit SNTP-basierte Dienste, z. B. Windows 2000 unterstützt jedoch weiterhin.  
  
### <a name="network-time-protocol"></a>Network Time Protocol  
(NTP = Network Time Protocol) ist der Standard time-Synchronisierungsprotokoll, die von der Windows-Zeitdienst im Betriebssystem verwendet. NTP ist eine fehlertolerante, hochgradig skalierbaren Time-Protokoll und das Protokoll für die Synchronisierung von Computertakt mithilfe eines Verweises festgelegten Zeit am häufigsten verwendeten.  
  
NTP-zeitsynchronisierung findet über einen Zeitraum und die Übertragung der NTP-Pakete über ein Netzwerk umfasst. NTP-Pakete enthalten Zeitstempel, die aus dem Client und dem Server, die Teil einer Zeit-Beispiel in der zeitsynchronisierung einschließen.  
  
NTP basiert auf Verweis Uhr, am genauesten Zeiträume verwendet werden, und alle Uhren in einem Netzwerk, Referenzuhr synchronisiert. NTP verwendet Coordinated Universal Time (UTC) als universelle Standard für die aktuelle Uhrzeit. UTC-Zeit ist unabhängig von Zeitzonen und NTP an einer beliebigen Stelle in der ganzen Welt, unabhängig von zeitzoneneinstellungen verwendet werden kann.  
  
#### <a name="ntp-algorithms"></a>NTP-Algorithmen  
NTP umfasst zwei Algorithmen, einen Algorithmus Uhr-Filterung und eine Uhr-Auswahlalgorithmus, bei der Windows-Zeitdienst, bei der Bestimmung der besten Zeit-Beispiel. Der Algorithmus Uhr-Filterung Stichproben gesichtet, die aus der abgefragten Zeitquellen empfangen werden, und bestimmen die beste Zeit Beispiele aus der jeweiligen Quelle dient. Die-Uhr-Auswahlalgorithmus bestimmt dann die genauesten Zeitserver im Netzwerk. Diese Informationen ist dann für den Algorithmus des Uhr Disziplin, übergeben, um die lokale Uhr des Computers an, zu korrigieren, während Fehler aufgrund von Latenz und Computer Uhr Ungenauigkeit von Netzwerk kompensiert gesammelten Informationen.  
  
Die NTP-Algorithmen sind unter Umständen von Licht bis mittlere Netzwerk- und lädt die genauesten. Wie bei jeder Algorithmus, der netzwerkübertragungszeit berücksichtigt, möglicherweise NTP-Algorithmen unter der Bedingung der extreme netzwerküberlastung unbefriedigend. Weitere Informationen zu den NTP-Algorithmen finden Sie unter RFC 1305 in der IETF RFC-Datenbank.  
  
#### <a name="ntp-time-provider"></a>NTP-Zeitanbieter  
Der Windows-Zeitdienst ist ein Abschlusszeit-Synchronisierung-Paket, das eine Vielzahl von Hardwaregeräten und Zeit Protokolle unterstützen kann. Um diese Unterstützung zu aktivieren, verwendet der Dienst austauschbare Zeitanbieter. Ein Zeitanbieter ist für die entweder um genaue Zeitstempel (aus dem Netzwerk oder von der Hardware) oder für die Bereitstellung dieser Zeitstempel auf anderen Computern über das Netzwerk verantwortlich.  
  
Der NTP-Anbieter ist der Normalzeit-Anbieter, die mit dem Betriebssystem enthalten. Der NTP-Anbieter entspricht der NTP-Version 3 für einen Client und Server gemäß Standards und SNTP-Clients und-Server für die Abwärtskompatibilität mit Windows 2000 und anderen SNTP-Clients interagieren kann. Der NTP-Anbieter in der Windows-Zeitdienst besteht aus den folgenden zwei Teilen:  
  
-   **NtpServer Ausgabe-Anbieter.** Dies ist ein Zeitserver, der auf Client-Zeit-Anforderungen im Netzwerk reagiert.  
  
-   **NtpClient Eingabeprovider.** Dies ist ein Zeit-Client, der Zeit aus einer anderen Quelle und ein Hardwaregerät oder einen NTP-Server abgerufen, und Beispiele für die Zeit, für die Synchronisierung der lokalen Uhr sind, zurückgeben kann.  
  
Obwohl die tatsächlichen Vorgänge dieser zwei Anbieter eng miteinander verknüpft sind, werden sie unabhängig mit dem Zeitdienst angezeigt. Ab Windows 2000 Server bei ein Windows-Computer mit einem Netzwerk verbunden ist, wird er als NTP-Client konfiguriert. Darüber hinaus Dienst zur Windows-Computern nur versucht, die Zeit wird standardmäßig mit einem Domänencontroller oder einer manuell angegebene Zeitquelle synchronisieren. Dies sind die bevorzugte Zeit-Anbieter, da sie automatisch zur Verfügung, sichere Quellen Zeit sind.  
  
#### <a name="ntp-security"></a>NTP Security  

Innerhalb der AD DS-Gesamtstruktur verwendet der Windows-Zeitdienst Standarddomäne-Sicherheitsfeatures für die Authentifizierung von Zeitdaten zu erzwingen. Die Sicherheit der NTP-Pakete, die gesendet werden, zwischen einem Domänenmitgliedscomputer und einem lokalen Domänencontroller, der als einen Zeitserver fungiert basiert auf gemeinsam verwendete Schlüsselauthentifizierung. Der Windows-Zeitdienst verwendet des Computers Kerberos-Sitzungsschlüssel, um authentifizierte Signaturen auf NTP-Pakete zu erstellen, die über das Netzwerk gesendet werden. NTP-Pakete werden nicht in den Anmeldedienst sicheren Kanal übertragen. Stattdessen bei der ein Computer die Zeit von einem Domänencontroller in der Domänenhierarchie anfordert, muss der Windows-Zeitdienst Zeitpunkt authentifiziert werden. Der Domänencontroller gibt dann die erforderliche Informationen zurück, in Form von einer 64-Bit-Wert, der mit dem Sitzungsschlüssel aus der Netlogon-Dienst authentifiziert wurde. Wenn das zurückgegebene NTP-Paket nicht mit des Computers auf Clientbasis signiert ist oder nicht ordnungsgemäß signiert ist, wird die Zeit abgelehnt. Solche Authentifizierungsfehler auftreten, werden im Ereignisprotokoll protokolliert. Auf diese Weise bietet der Windows-Zeitdienst Sicherheit NTP-Daten in einer AD DS-Gesamtstruktur.  
  
Im Allgemeinen beziehen Windows-zeitclients automatisch genaue Uhrzeit für die Synchronisierung von Domänencontrollern in der gleichen Domäne. In einer Gesamtstruktur synchronisieren die Domänencontroller einer untergeordneten Domäne Zeit mit Domänencontrollern in Domänen. Wenn Sie ein Zeitserver ein authentifiziertes NTP-Pakets an einen Client zurückgegeben, die die Zeit anfordert, ist das Paket über einen Kerberos-Sitzungsschlüssel, der durch ein domänenübergreifendes Vertrauenskonto definiert signiert. Die Vertrauenskonto wird erstellt, wenn eine neue AD DS-Domäne eine Gesamtstruktur verknüpft, und der Netlogon-Dienst den Sitzungsschlüssel verwaltet. Auf diese Weise wird der Domänencontroller, der als zuverlässige, in der Gesamtstruktur-Stammdomäne konfiguriert ist die authentifizierte Zeitquelle für alle Domänencontroller in der über- und untergeordneten Domänen und indirekt für alle Computer, die sich in der Struktur von Domäne befinden.  
  
Der Windows-Zeitdienst kann für die Zusammenarbeit zwischen Gesamtstrukturen konfiguriert werden, aber es ist wichtig zu beachten, dass diese Konfiguration nicht sicher ist. Ein NTP-Server kann z. B. in einer anderen Gesamtstruktur verfügbar sein. Da dieser Computer in einer anderen Gesamtstruktur ist, besteht jedoch keine Kerberos-Sitzungsschlüssel mit dem Signieren und NTP-Pakete zu authentifizieren. Um genaue uhrzeitsynchronisierung von einem Computer in einer anderen Gesamtstruktur zu erhalten, der Client benötigt Netzwerkzugriff auf diesem Computer aus, und der Zeitdienst muss konfiguriert werden, um eine bestimmte Zeitquelle befindet sich in der anderen Gesamtstruktur zu verwenden. Wenn ein Client von einem NTP-Server außerhalb der eigenen Domänenhierarchie manuell zum Zeitpunkt des Zugriffs konfiguriert ist, wird die NTP-Pakete, die zwischen dem Client und der Zeitserver gesendet werden nicht authentifiziert, und sind daher nicht sicher. Auch bei der Implementierung von Gesamtstruktur-Vertrauensstellungen ist der Windows-Zeitdienst nicht gesamtstrukturübergreifend sicher. Obwohl der Anmeldedienst sichere Kanal der Authentifizierungsmechanismus für den Windows-Zeitdienst ist, wird die gesamtstrukturübergreifende Authentifizierung nicht unterstützt.  
  
#### <a name="hardware-devices-that-are-supported-by-the-windows-time-service"></a>Hardwaregeräten, die von der Windows-Zeitdienst unterstützt werden  
Hardware-basierte Uhren, z. B. GPS oder Optionsfelder Uhren werden häufig als äußerst präzise Verweis Uhr Geräte verwendet. Standardmäßig die Windows Time Service NTP Zeitanbieter unterstützt keine direkte Verbindung von einem Hardwaregerät auf einem Computer, obwohl es möglich ist, ein softwarebasierter unabhängige Zeitanbieter erstellen, die diese Art von Verbindung unterstützt. Diese Art von in Verbindung mit der Windows-Zeitdienst-Anbieter bieten eine zuverlässige und stabile Zeitverweis an.  
  
Hardwaregeräte, wie z. B. eine Cesium Uhr oder einen Empfänger globalen Positionsbestimmungssystems (GPS) bieten genaue, aktuelle Uhrzeit gemäß der als Standard eine genaue Definition von Zeit zu erhalten. Cesium Uhren extrem stabil sind und von Faktoren wie z. B. Temperatur, Luftdruck und Luftfeuchtigkeit nicht betroffen sind, aber auch sehr teuer werden. Ein GPS-Empfänger ist sehr viel weniger kostspielig im Betrieb und auch eine genaue Verweis Uhr. GPS-Empfänger erhalten die Uhrzeit von Satelliten, die ihre Zeit mit einer Uhr Cesium zu erhalten. Ohne die Verwendung eines unabhängigen Zeit-Anbieters können Windows-Zeitserver Zeit abrufen, indem Herstellen einer Verbindung mit einem externen NTP-Server, der mit einem Hardwaregerät über ein Telefon oder dem Internet verbunden ist. Organisationen wie der U.s. Naval Observatory bieten NTP-Server, die mit äußerst zuverlässig Verweis Uhren verbunden sind.  
  
Viele GPS-Empfänger und anderen Geräten Zeit können als NTP-Server in einem Netzwerk fungieren. Sie können konfigurieren, dass Ihre AD DS-Gesamtstruktur, um aus diesen externen Hardwaregeräten zu synchronisieren, nur dann, wenn sie auch als NTP-Server in Ihrem Netzwerk fungieren. Zu diesem Zweck konfigurieren Sie den Domänencontroller fungiert als dem primären Domänencontroller (PDC)-Emulator in Ihrer Gesamtstruktur-Stammdomäne zum Synchronisieren mit dem NTP-Server, die vom GPS-Gerät bereitgestellt. Zu diesem Zweck finden Sie unter [konfigurieren den Windows-Zeitdienst auf dem PDC-Emulator in der Gesamtstruktur-Stammdomäne](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29).  
  
### <a name="simple-network-time-protocol"></a>Simple Network Time Protocol  
Simple Network Time Protocol (SNTP) ist ein vereinfachtes Zeit, die für Server und Clients, die nicht den Grad an Genauigkeit erfordern, die NTP bietet vorgesehen ist. SNTP, eine weitere rudimentäre Version NTP, ist das primäre Time-Protokoll, das in Windows 2000 verwendet wird. Da die Netzwerk-Paket-Formate von SNTP und NTP identisch sind, sind die beiden Protokolle interoperabel. Der Hauptunterschied zwischen den beiden ist, dass SNTP keine die fehlerverwaltung und komplexe für Inhaltsfiltersysteme sind, die NTP bereitstellt. Weitere Informationen zu Simple Network Time Protocol finden Sie unter RFC 1769 in der IETF RFC-Datenbank.  
  
### <a name="time-protocol-interoperability"></a>Protokollinteroperabilität Zeit  
Der Windows-Zeitdienst kann in einer gemischten Umgebung aus Computern unter Windows 2000, Windows XP und Windows Server 2003 ausgeführt werden, da das in Windows 2000 verwendete SNTP-Protokoll mit dem NTP-Protokoll in Windows XP und Windows Server 2003 kompatibel ist.  
  
Der Zeitdienst in Windows NT Server 4.0, namens TimeServ, synchronisiert die Uhrzeit in einem Windows NT 4.0-Netzwerk. TimeServ ist ein Add-on-Feature, das als Teil der *Microsoft Windows NT 4.0 Resource Kit* und bietet keinen den Grad der Zuverlässigkeit der zeitsynchronisierung, die von Windows Server 2003 erforderlich ist.  
  
Der Windows-Zeitdienst kann zusammenarbeiten, mit Computern unter Windows NT 4.0, da sie Zeit mit Windows 2000 oder Windows Server 2003-Computern synchronisiert werden können; ein Computer unter Windows 2000 oder Windows Server 2003 jedoch nicht automatisch auf Windows NT 4.0-Zeitserver ermittelt. Angenommen, Sie verfügen über Wenn Ihre Domäne so konfiguriert ist, dass die zeitsynchronisierung mit der Domäne Hierarchiebasierte-Methode der Synchronisierung aus, und Sie möchten für Computer in der Domänenhierarchie, Uhrzeit mit einem Windows NT 4.0-Domänencontroller zu synchronisieren, Konfiguration die Computer manuell, um mit der Windows NT 4.0-Domänencontroller zu synchronisieren.  
  
Windows NT 4.0 verwendet einen einfacheren Mechanismus für die zeitsynchronisierung als der Zeit von Windows-Dienst verwendet. Aus diesem Grund wird um genaue uhrzeitsynchronisierung in Ihrem Netzwerk zu gewährleisten, empfohlen, alle Windows NT 4.0-Domänencontroller auf Windows 2000 oder Windows Server 2003 zu aktualisieren.  
  
## <a name="windows-time-service-processes-and-interactions"></a>Windows Time Serviceprozesse und-Interaktionen  

Der Windows-Zeitdienst wurde entwickelt, um die Uhren von Computern in einem Netzwerk zu synchronisieren. Der Netzwerk-Zeit-Synchronisierungsvorgang Zeit konvergent, so genannte tritt auf, in einem Netzwerk immer greift auf Computer aus eine genauere Zeitserver. Zeit Konvergenz umfasst einen Prozess mit dem ein autorisierender Server die aktuelle Uhrzeit auf den Clientcomputern in Form von NTP-Pakete enthält. Die Informationen in einem Paket gibt an, ob eine Anpassung der aktuellen-Uhrzeit des Computers vorgenommen werden, damit er mit dem eine präzisere-Server synchronisiert wird.  
  
Versuchen als Teil des Prozesses Konvergenz Zeit Mitglieder der Domäne, die zeitsynchronisierung mit einem beliebigen Domänencontroller in derselben Domäne befindet sich ein. Wenn der Computer ein Domänencontroller ist, versucht, die mit einem mehr autorisierenden Domänencontroller zu synchronisieren.  
  
Computer unter Windows XP Home Edition oder Computer, die nicht zu einer Domäne verknüpft sind, versuchen Sie nicht zum Synchronisieren mit der Domänenhierarchie, aber sind standardmäßig so konfiguriert, um Zeit zu ermitteln, von "Time.Windows.com".  
  
Um einem Computer unter Windows Server 2003 als autorisierend herzustellen, muss der Computer konfiguriert werden, werden von einer zuverlässigen Zeitquelle. Standardmäßig ist der erste Domänencontroller, der in einer Windows Server 2003-Domäne installiert ist automatisch für werden von einer zuverlässigen Zeitquelle konfiguriert. Da es auf dem autorisierenden Computer für die Domäne ist, muss es zum Synchronisieren von mit einer externen Zeitquelle und nicht mit der Domänenhierarchie konfiguriert werden. Außerdem werden standardmäßig alle Mitglieder anderer Windows Server 2003-Domäne konfiguriert, für die Synchronisierung mit der Domänenhierarchie.  
  
Nachdem Sie ein Windows Server 2003-Netzwerk hergestellt haben, können Sie den Windows-Zeitdienst Verwendung eines der folgenden Optionen für die Synchronisierung konfigurieren:  
  
-   Hierarchie-basierte domänensynchronisierung  
  
-   Eine manuell konfigurierte Synchronisierungsquelle  
  
-   Alle verfügbaren Synchronisierungsmechanismen  
  
-   Keine Synchronisierung.  
  
Jeder dieser Typen von Synchronisierung wird im folgenden Abschnitt erläutert.  
  
### <a name="domain-hierarchy-based-synchronization"></a>Hierarchie-basierte Domänensynchronisierung  

Synchronisierung, die in einer Domänenhierarchie basiert verwendet die Hierarchie der AD DS-Domäne, um eine zuverlässige Quelle für die Synchronisierung von Zeit zu suchen. Basierend auf Domänenhierarchie, bestimmt der Windows-Zeitdienst die Genauigkeit jedes Mal-Servers. In einer Gesamtstruktur mit Windows Server 2003 enthält die Computer mit der primären Domänencontrollers (PDC) Emulator Betriebsmasterfunktion, befindet sich in der Gesamtstruktur-Stammdomäne, die Position der beste Zeitpunkt, an, es sei denn, eine andere zuverlässige Zeitquelle konfiguriert wurde. Die folgende Abbildung veranschaulicht einen Pfad für die zeitsynchronisierung zwischen Computern in einer Domänenhierarchie.  
  
**Zeitsynchronisierung in einer AD DS-Hierarchie**  
![Windows Time](../media/Windows-Time-Service/How-the-Windows-Time-Service-Works/trnt_ntw_adhc.gif)
  
#### <a name="reliable-time-source-configuration"></a>Konfigurieren einer zuverlässigen Zeitquelle  
Ein Computer, der einer zuverlässigen Zeitquelle konfiguriert ist, wird als Stamm der Zeitdienst identifiziert. Der Stamm des Zeitdiensts ist der autorisierenden Server für die Domäne und in der Regel ist so konfiguriert, dass Zeit aus einer externen NTP-Server oder ein Hardwaregerät abrufen. Ein Zeitserver kann konfiguriert werden, als einer zuverlässigen Zeitquelle optimieren, wie Zeit innerhalb der gesamten Domänenhierarchie übertragen wird. Wenn ein Domänencontroller konfiguriert ist, werden von einer zuverlässigen Zeitquelle, kündigt Netlogon-Dienst diesen Domänencontroller als einer zuverlässigen Zeitquelle, bei der Anmeldung mit dem Netzwerk. Wenn einer Zeitquelle synchronisieren mit anderen Domänencontrollern gesucht werden soll, wählen sie eine zuverlässige Quelle zuerst, wenn eine verfügbar ist.  
  
#### <a name="time-source-selection"></a>Zeitauswahl-Quelle  
Die Zeit Auswahl Quellprozess kann zwei Probleme in einem Netzwerk erstellen:  
  
-   Zusätzliche Synchronisierung wechselt.  
  
-   Erhöhter Volumen des Netzwerkverkehrs.  
  
Ein Zyklus in das Netzwerk für die Synchronisierung tritt auf, wenn Zeit mehr übrig eine Gruppe von Domänencontrollern konsistent ist und gleichzeitig genutzt fortlaufend ohne eine erneute Synchronisierung mit einem anderen zuverlässigen Zeitquelle gemeinsam. Der Windows-Zeitdienst Zeit Quelle Auswahlalgorithmus dient zum Schutz vor dieser Art von Problemen.  
  
Ein Computer, die eine der folgenden Methoden zum Identifizieren einer Zeitquelle synchronisieren mit verwendet:  
  
-   Wenn der Computer nicht Mitglied einer Domäne ist, müssen sie für die Synchronisierung mit einer angegebenen Zeitquelle konfiguriert werden.  
  
-   Wenn der Computer auf einem Mitgliedsserver oder Arbeitsstation innerhalb einer Domäne in der Standardeinstellung wird anschließend die AD DS-Hierarchie und synchronisiert seine Zeit mit einem Domänencontroller in der lokalen Domäne, die gerade den Windows-Zeitdienst ausgeführt wird.  
  
Wenn der Computer ein Domänencontroller ist, ist es bis zu sechs Abfragen an die Synchronisierung mit einem anderen Domänencontroller zu suchen. Jede Abfrage ist so konzipiert, um eine Zeitquelle mit bestimmten Attributen, z. B. eine Art von Domänencontroller an einem bestimmten Ort zu identifizieren und davon, ob es einer zuverlässigen Zeitquelle ist. Die Datenquelle für die Zeit muss auch die folgenden Einschränkungen entsprechen:  
  
-   Eine zuverlässigen Zeitquelle kann nur mit einem Domänencontroller in der übergeordneten Domäne synchronisieren.  
  
-   PDC-Emulator kann mit einer zuverlässigen Zeitquelle in seiner eigenen Domäne oder einen beliebigen Domänencontroller in der übergeordneten Domäne synchronisieren.  
  
Ist der Domänencontroller nicht mit dem Typ des Domänencontrollers synchronisiert werden, die sie Abfragen ist, wird die Abfrage nicht vorgenommen werden. Der Domänencontroller weiß, welche Art von Computer, die sie aus abrufen kann, bevor sie die Abfrage stellt. Z. B. versucht lokaler PDC-Emulator in Abfrage Zahlen, drei oder sechs nicht, da ein Domänencontroller nicht versucht, eine Synchronisierung mit sich selbst.  
  
Die folgende Tabelle enthält die Abfragen, die von einem Domänencontroller wird eine Zeitquelle und die Reihenfolge, in der die Abfragen erfolgen.  
  
**Abfragen der Domäne Domänencontroller-Zeitquelle**  
  
|Abfrageanzahl|Domänencontroller|Speicherort|Zuverlässigkeit von Zeitquelle|  
|----------------|---------------------|------------|------------------------------|  
|1|Übergeordneten Domänencontroller|Am Standort|Bevorzugt eine zuverlässige Zeitquelle jedoch mit einer nicht zuverlässigen Zeitquelle synchronisieren können, wenn dies alles ist, die verfügbar ist.|  
|2|Lokale Domänencontroller|Am Standort|Nur synchronisiert mit einer zuverlässigen Zeitquelle.|  
|3|Lokale PDC-emulator|Am Standort|Ist nicht gültig.<br /><br />Ein Domänencontroller versucht nicht, die Synchronisierung mit sich selbst.|  
|4|Übergeordneten Domänencontroller|Außerhalb des Standorts|Bevorzugt eine zuverlässige Zeitquelle jedoch mit einer nicht zuverlässigen Zeitquelle synchronisieren können, wenn dies alles ist, die verfügbar ist.|  
|5|Lokale Domänencontroller|Außerhalb des Standorts|Nur synchronisiert mit einer zuverlässigen Zeitquelle.|  
|6|Lokale PDC-emulator|Außerhalb des Standorts|Ist nicht gültig.<br /><br />Ein Domänencontroller versucht nicht, die Synchronisierung mit sich selbst.| 
  
**Hinweis**  
  
-   Ein Computer synchronisiert sich nie mit sich selbst. Wenn der Computer, die versuchen, die Synchronisierung der lokalen PDC-Emulator ist, versucht es nicht Abfragen 3 oder 6.  
  
Jede Abfrage gibt eine Liste der Domänencontroller, die als Zeitquelle verwendet werden kann. Windows Time weist abgefragt jeden Domänencontroller, die ein Ergebnis basierend auf die Zuverlässigkeit und den Standort des Domänencontrollers. Die folgende Tabelle enthält die Ergebnisse von Windows-Zeit für jede Art von Domänencontroller zugewiesen wird.  
  
**Bestimmung der Bewertung**  
  
|Domänencontrollerstatus|Wert|  
|----------------------------|---------|  
|Domänencontroller befindet sich am gleichen Standort|8|  
|Domänencontroller, die als von einer zuverlässigen Zeitquelle|4|  
|Domänencontroller befindet sich in der übergeordneten Domäne|2|  
|Domänencontroller, ist der PDC-emulator|1|  
  
Wenn der Windows-Zeitdienst feststellt, dass sie den Domänencontroller mit der best möglichen Bewertung identifiziert hat, erfolgen keine weiteren Abfragen. Die Ergebnisse, die durch den Zeitdienst zugewiesen sind kumulativ, was bedeutet, dass die PDC-Emulator an demselben Standort befindet sich eine Bewertung von neun empfängt.  
  
Wenn der Stamm des Diensts Zeit nicht für die Synchronisierung mit einer externen Datenquelle konfiguriert ist, steuert die interne Hardware Uhr des Computers die Zeit an.  
  
### <a name="manually-specified-synchronization"></a>Manuell konfigurierte Synchronisierung  
Manuell konfigurierte Synchronisierung können Sie festlegen, ein einzelner Peer oder eine Liste von Peers, die aus denen Aufruf von ein Computer abruft. Wenn der Computer nicht Mitglied einer Domäne ist, müssen sie manuell konfiguriert werden, um mit einer angegebenen Zeitquelle synchronisieren. Ein Computer, dass ein Mitglied einer Domäne wird standardmäßig für die Synchronisierung von der Domänenhierarchie konfiguriert ist, ist die Synchronisierung manuell konfigurierte besonders hilfreich, für den Stamm der Gesamtstruktur der Domäne oder für Computer, die nicht zu einer Domäne verknüpft sind. Bietet eine zuverlässige Zeit manuelle Eingabe einen externen NTP-Server mit dem autorisierenden Computer für Ihre Domäne zu synchronisieren. Konfigurieren der autorisierenden Computers für Ihre Domäne für die Synchronisierung mit einer Hardware-Uhr ist jedoch tatsächlich eine bessere Lösung für die präziseste, sichere Zeit mit der Domäne bereitstellen.  
  
Manuell konfigurierte Datenquellen werden nicht authentifiziert werden, es sei denn, die ein bestimmten Zeitpunkt-Anbieter für sie geschrieben wurde und sie sind daher anfällig für Angriffe. Wenn ein Computer mit einer Quelle manuell konfigurierte anstelle der authentifizierende Domänencontroller synchronisiert wird, können auch die beiden Computer nicht mehr synchronisiert, die Kerberos-Authentifizierung einen Fehler verursacht sein. Dies kann dazu führen, dass andere Aktionen, die Netzwerkauthentifizierung fehlschlägt, z. B. drucken oder Freigeben von Dateien. Wenn nur der Gesamtstruktur-Stammdomäne für die Synchronisierung mit einer externen Datenquelle konfiguriert ist, bleiben allen anderen Computern in der Gesamtstruktur synchronisiert miteinander, sodass Replay-Angriffe zu schwierig.  
  
### <a name="all-available-synchronization-mechanisms"></a>Alle verfügbaren Synchronisierungsmechanismen  

Die Option "alle verfügbaren Synchronisierungsmechanismen" ist besonders hilfreich, Synchronisierungsmethode für Benutzer in einem Netzwerk. Diese Methode ermöglicht die Synchronisierung mit der Domänenhierarchie und möglicherweise auch einen alternativen Zeitquelle, wenn die Domänenhierarchie nicht verfügbar, abhängig von der Konfiguration ist. Wenn der Client kann nicht mit der Domänenhierarchie zeitsynchronisierung ist, die Zeitquelle automatisch fragt die Zeitquelle gemäß der **NtpServer** festlegen. Diese Methode der Synchronisierung ist wahrscheinlich auf die genaue Zeit für Clients bereitzustellen.  

### <a name="stopping-time-synchronization"></a>Beenden der Zeitsynchronisierung  
Es gibt bestimmte Situationen, in denen Sie eine Synchronisierung der Uhrzeit des Computers beenden möchten. Wenn ein Computer versucht, die über eine DFÜ-Verbindung mit einer Zeitquelle im Internet oder von einem anderen Standort über ein WAN synchronisieren, können sie z. B. teure Telefongebühren anfallen. Wenn Sie die Synchronisierung auf diesem Computer deaktivieren, zu verhindern, dass Sie den Computer versucht, die eine Zeitquelle über eine DFÜ-Verbindung zugreifen.  
  
Sie können auch die Synchronisierung, um zu verhindern, dass die Generierung von Fehlern im Ereignisprotokoll deaktivieren. Jedes Mal, wenn ein Computer versucht, die mit einer Zeitquelle synchronisieren, die nicht verfügbar ist, generiert es einen Fehler im Ereignisprotokoll. Wenn eine Zeitquelle, auf das Netzwerk für die geplante Wartung verwendet wird, und Sie nicht den Client für die Synchronisierung von einer anderen Quelle neu konfigurieren möchten, können Sie die Synchronisierung auf dem Client zu verhindern, dass es versucht, die Synchronisierung während der Zeitserver deaktivieren. ist nicht verfügbar.  
  
Es ist nützlich, um die Synchronisierung auf dem Computer zu deaktivieren, das als Stammverzeichnis für das Netzwerk für die Synchronisierung festgelegt ist. Dies gibt an, dass der Root-Computer, die lokale Uhr vertraut. Wenn der Stamm der Hierarchie für die Synchronisierung nicht, um festgelegt ist **NoSync** und wenn sie mit der eine andere Zeitquelle synchronisieren kann, Clients akzeptieren keine das Paket, das diesen Computer gesendet, da die Zeit nicht vertrauenswürdig ist.
  
Einmalig sind Server, die von Clients als vertrauenswürdig eingestuft werden, auch wenn sie nicht mit einem anderen Zeitquelle synchronisiert haben, die vom Client als zuverlässige Zeitserver identifiziert wurden.  
  
### <a name="disabling-the-windows-time-service"></a>Deaktivieren des Windows-Zeitdienstes  
Der Windows-Zeitdienst (W32Time) kann vollständig deaktiviert werden. Wenn Sie entscheiden, ein Drittanbieter-Time-Synchronisierung-Produkt zu implementieren, die NTP-Server verwendet, müssen Sie den Windows-Zeitdienst deaktivieren. Dies ist, da alle NTP-Server Zugriff auf TCP-Port 123 User Datagram Protocol (UDP benötigen) aus, und wie der Windows-Zeitdienst auf dem Windows Server 2003-Betriebssystem ausgeführt wird, Port 123 durch Windows-Uhrzeit reserviert bleibt.  
  
## <a name="network-ports-used-by-windows-time-service"></a>Von Windows-Zeitdienst verwendete Netzwerkports  
Der Windows-Zeitdienst kommuniziert über ein Netzwerk für den zuverlässigen Quellen zu identifizieren, erhalten Informationen und Informationen mit anderen Computern bereitstellen. Er führt diese Kommunikation über die NTP und SNTP-RFCs definiert.  
  
**Portzuweisungen für den Windows-Zeitdienst**  
  
|Dienstname|UDP|TCP|  
|----------------|-------|-------|  
|NTP|123|Nicht zutreffend|  
|SNTP|123|Nicht zutreffend|  
  
## <a name="see-also"></a>Siehe auch  
[Technische Referenz für Windows Time Service](windows-time-service-tech-ref.md)
[Windows-Zeitdienst: Tools und Einstellungen](Windows-Time-Service-Tools-and-Settings.md)
[Microsoft Knowledge Base-Artikel 902229](https://go.microsoft.com/fwlink/?LinkId=186066)