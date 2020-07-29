---
ms.assetid: d1953097-63ea-4a0e-b860-2f3b7c175c41
title: Funktionsweise des Windows-Zeitdiensts
author: dcuomo
ms.author: dacuo
manager: dougkim
ms.date: 05/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: c1c0356e834f01967959fb804f477641f8ce0314
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182126"
---
# <a name="how-the-windows-time-service-works"></a>Funktionsweise des Windows-Zeitdiensts

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 oder höher

**In diesem Abschnitt**

-   [Windows-Zeitdienst: Architektur](#windows-time-service-architecture)

-   [Windows-Zeitdienst: Zeitprotokolle](#windows-time-service-time-protocols)

-   [Windows-Zeitdienst: Prozesse und Interaktionen](#windows-time-service-processes-and-interactions)

-   [Vom Windows-Zeitdienst verwendete Netzwerkports](#network-ports-used-by-windows-time-service)

> [!NOTE]
> In diesem Thema wird ausschließlich erläutert, wie der Windows-Zeitdienst (W32Time) funktioniert. Informationen zum Konfigurieren des Windows-Zeitdiensts findest du unter [Konfigurieren von Systemen für hohe Genauigkeit](configuring-systems-for-high-accuracy.md).

> [!NOTE]
> In Windows Server 2003 und Microsoft Windows 2000 Server heißt der Verzeichnisdienst Active Directory-Verzeichnisdienst. In Windows Server 2008 und höheren Versionen heißt der Verzeichnisdienst Active Directory Domain Services (AD DS). Im weiteren Verlauf dieses Themas wird Bezug auf AD DS genommen, die Informationen gelten jedoch auch für Active Directory.

Obwohl es sich beim Windows-Zeitdienst nicht um eine exakte Implementierung des Netzwerkzeitprotokolls (Network Time Protocol, NTP) handelt, verwendet er die komplexe Suite von Algorithmen, die in den NTP-Spezifikationen definiert sind, um sicherzustellen, dass Uhren auf Computern innerhalb eines Netzwerks so genau wie möglich sind. Im Idealfall werden alle Computeruhren in einer AD DS-Domäne mit der Zeit eines autoritativen Computers synchronisiert. In einem Netzwerk können sich viele Faktoren auf die Zeitsynchronisierung auswirken. Die folgenden Faktoren wirken sich häufig auf die Genauigkeit der Synchronisierung in AD DS aus:

-   Netzwerkbedingungen

-   Die Genauigkeit der Hardwareuhr des Computers

-   Die Menge an CPU- und Netzwerkressourcen, die für den Windows-Zeitdienst verfügbar sind

> [!IMPORTANT]
> Vor Windows Server 2016 war der W32Time-Dienst nicht so konzipiert, dass er die Anforderungen zeitabhängiger Anwendungen erfüllte.  Updates für Windows Server 2016 ermöglichen es jetzt jedoch, eine Lösung für eine Genauigkeit von 1 ms in deiner Domäne zu implementieren.  Weitere Informationen findest du unter [Windows 2016: Genaue Zeit](accurate-time.md) und [Supportgrenze zum Konfigurieren des Windows-Zeitdiensts für Umgebungen mit hoher Genauigkeit](support-boundary.md).

Computer, die ihre Zeit seltener synchronisieren oder keiner Domäne beigetreten sind, werden standardmäßig so konfiguriert, dass sie sich mit „time.windows.com“ synchronisieren.  Daher ist es nicht möglich, die Zeitgenauigkeit auf Computern zu gewährleisten, die nur über vorübergehende oder gar keine Netzwerkverbindungen verfügen.

Eine AD DS-Gesamtstruktur verfügt über eine vorgegebene Zeitsynchronisierungshierarchie. Der Windows-Zeitdienst synchronisiert die Zeit zwischen den Computern innerhalb der Hierarchie mit den genauesten Referenzuhren auf der obersten Ebene der Hierarchie. Wenn auf einem Computer mehr als eine Zeitquelle konfiguriert ist, verwendet der Windows-Zeitdienst NTP-Algorithmen, um die beste Zeitquelle aus den konfigurierten Quellen auszuwählen, und zwar basierend auf der Fähigkeit des Computers, sich mit dieser Zeitquelle zu synchronisieren. Der Windows-Zeitdienst unterstützt keine Netzwerksynchronisierung von Broadcast- oder Multicastpeers. Weitere Informationen zu diesen NTP-Funktionen findest du im RFC 1305 in der IETF RFC-Datenbank.

Jeder Computer, auf dem der Windows-Zeitdienst ausgeführt wird, verwendet den Dienst, um die genaueste Zeit aufrechtzuerhalten. Computer, die Mitglieder einer Domäne sind, fungieren standardmäßig als Zeitclient. Daher ist es in den meisten Fällen nicht erforderlich, den Windows-Zeitdienst zu konfigurieren. Der Windows-Zeitdienst kann jedoch so konfiguriert werden, dass er Zeit von einer festgelegten Referenzzeitquelle anfordert, und er kann auch Clients die Zeit bereitstellen.

Der Grad, in dem die Zeit eines Computers genau ist, wird als Stratum bezeichnet. Die genaueste Zeitquelle in einem Netzwerk (z. B. eine Hardwareuhr) belegt die niedrigste Stratumstufe, also „Stratum 1“. Diese genaue Zeitquelle wird als Referenzuhr bezeichnet. Ein NTP-Server, der seine Zeit direkt von einer Referenzuhr bezieht, belegt ein Stratum, das eine Ebene höher ist als das der Referenzuhr. Ressourcen, die ihre Zeit vom NTP-Server beziehen, sind zwei Stufen von der Referenzuhr entfernt und belegen deshalb ein Stratum, das sich zwei Stufen über der genauesten Zeitquelle befindet usw. Mit steigender Nummer des Stratums eines Computers kann die Zeit seiner Systemuhr ungenauer werden. Daher ist die Stratumstufe eines Computers ein Indikator dafür, wie eng dieser Computer mit der genauesten Zeitquelle synchronisiert wird.

Wenn der W32Time-Manager Zeitstichproben empfängt, verwendet er spezielle Algorithmen in NTP, um zu bestimmen, welche der Zeitstichproben am besten zur Verwendung geeignet ist. Der Zeitdienst verwendet außerdem einen weiteren Satz von Algorithmen, um zu bestimmen, welche der konfigurierten Zeitquellen die genaueste ist. Wenn der Zeitdienst ermittelt hat, welche Zeitstichprobe am besten ist, passt er auf Grundlage der oben genannten Kriterien die lokale Taktfrequenz der Uhr so an, dass sie in Richtung der richtigen Zeit konvergiert. Wenn die Zeitdifferenz zwischen der lokalen Uhr und der ausgewählten genauen Zeitstichprobe (auch als „Zeitabweichung“ bezeichnet) zu groß ist, um durch Anpassung der Taktrate der lokalen Uhr korrigiert zu werden, stellt der Zeitdienst die lokale Uhr auf die richtige Zeit ein. Diese Anpassung der Taktrate der Uhr bzw. die direkte Änderung der Uhrzeit wird als „Uhrdisziplin“ bezeichnet.

## <a name="windows-time-service-architecture"></a>Windows-Zeitdienst-Architektur
Der Windows-Zeitdienst besteht aus den folgenden Komponenten:

-   Dienststeuerungs-Manager

-   Windows-Zeitdienst-Manager

-   Uhrdisziplin

-   Zeitanbieter

In der folgenden Abbildung ist die Architektur des Windows-Zeitdiensts dargestellt.

**Windows-Zeitdienst: Architektur**

![Windows-Zeitdienst](../media/Windows-Time-Service/How-the-Windows-Time-Service-Works/trnt_sec_arcc.gif)

Der Dienststeuerungs-Manager ist für das Starten und Beenden des Windows-Zeitdiensts verantwortlich. Der Windows-Zeitdienst-Manager ist für das Initiieren der Aktion der im Betriebssystem enthaltenen NTP-Zeitanbieter verantwortlich. Der Windows-Zeitdienst-Manager steuert alle Funktionen des Windows-Zeitdiensts sowie die Zusammenführung aller Zeitstichproben. Zusätzlich zur Bereitstellung von Informationen über den aktuellen Systemzustand, wie z. B. die aktuelle Zeitquelle oder den Zeitpunkt der letzten Aktualisierung der Systemuhr, ist der Windows-Zeitdienst-Manager auch für das Erstellen von Ereignissen im Ereignisprotokoll verantwortlich.

Der Zeitsynchronisierungsprozess umfasst die folgenden Schritte:

-   Eingeben von Anbieteranforderungen und Empfangen von Zeitstichproben von konfigurierten NTP-Zeitquellen.

-   Diese Zeitstichproben werden dann an den Windows-Zeitdienst-Manager übergeben, der alle Stichproben sammelt und sie an die Uhrdisziplin-Unterkomponente übergibt.

-   Die Uhrdisziplin-Unterkomponente wendet die NTP-Algorithmen an, was zur Auswahl der besten Zeitstichprobe führt.

-   Die Uhrdisziplin-Unterkomponente passt die Zeit der Systemuhr an die genaueste Zeit an, indem entweder die Taktrate der Uhr angepasst oder die Uhrzeit direkt geändert wird.

Wenn ein Computer als Zeitserver festgelegt wurde, kann er die Zeit an einen beliebigen Computer weitersenden, der eine Zeitsynchronisierung zu einem beliebigen Zeitpunkt in diesem Vorgang anfordert.

## <a name="windows-time-service-time-protocols"></a>Windows-Zeitdienst: Zeitprotokolle

Mit Zeitprotokollen wird festgelegt, wie genau die Uhren von zwei Computern synchronisiert werden. Ein Zeitprotokoll ist dafür verantwortlich, die besten verfügbaren Zeitinformationen zu ermitteln und die Uhren konvergieren zu lassen, um sicherzustellen, dass auf separaten Systemen eine konsistente Zeit aufrechterhalten wird.

Der Windows-Zeitdienst verwendet das Netzwerkzeitprotokoll (NTP), um die Synchronisierung der Zeit über ein Netzwerk zu unterstützen. NTP ist ein Internetzeitprotokoll, das die für die Synchronisierung von Uhren erforderlichen Disziplinalgorithmen umfasst. NTP ist ein genaueres Zeitprotokoll als das Simple Network Time Protocol (SNTP), das in einigen Versionen von Windows verwendet wird. W32Time unterstützt jedoch weiterhin SNTP, um Abwärtskompatibilität mit Computern zu ermöglichen, auf denen SNTP-basierte Zeitdienste, wie beispielsweise Windows 2000, ausgeführt werden.

### <a name="network-time-protocol"></a>Netzwerkzeitprotokoll (NTP)
Das Netzwerkzeitprotokoll (NTP) ist das standardmäßige Protokoll für Zeitsynchronisierung, das vom Windows-Zeitdienst im Betriebssystem verwendet wird. NTP ist ein fehlertolerantes, hochgradig skalierbares Zeitprotokoll und ist das Protokoll, das am häufigsten für die Synchronisierung von Computeruhren mithilfe einer festgelegten Zeitreferenz verwendet wird.

Die NTP-Zeitsynchronisierung erfolgt über einen bestimmten Zeitraum und umfasst die Übertragung von NTP-Paketen über ein Netzwerk. NTP-Pakete enthalten Zeitstempel, die eine Zeitstichprobe von sowohl dem Client als auch vom Server enthalten, die an der Zeitsynchronisierung teilnehmen.

NTP verwendet eine Referenzuhr zum Definieren der genauesten Zeit, die verwendet werden soll, und synchronisiert alle Uhren in einem Netzwerk mit dieser Referenzuhr. NTP verwendet die koordinierte Weltzeit (UTC) als universellen Standard für die aktuelle Zeit. UTC ist unabhängig von Zeitzonen und ermöglicht, dass NTP unabhängig von den Zeitzoneneinstellungen überall auf der Welt verwendet werden kann.

#### <a name="ntp-algorithms"></a>NTP-Algorithmen
NTP umfasst zwei Algorithmen, einen Algorithmus zum Filtern von Uhren und Algorithmus zum Auswählen von Uhren, um dem Windows-Zeitdienst bei der Ermittlung der besten Zeitstichprobe zu helfen. Der Algorithmus zum Filtern von Uhren ist für das Durchsuchen von Zeitstichproben konzipiert, die von abgefragten Zeitquellen empfangen werden, und um die besten Zeitstichproben von jeder Quelle zu ermitteln. Der Algorithmus zum Auswählen von Uhren bestimmt dann den genauesten Zeitserver im Netzwerk. Diese Informationen werden dann an den Uhrdisziplinalgorithmus übergeben, der die gesammelten Informationen verwendet, um die lokale Uhr des Computers zu korrigieren, während gleichzeitig Fehler aufgrund von Netzwerklatenz und Ungenauigkeit der Computeruhr kompensiert werden.

Die NTP-Algorithmen sind am genauesten bei leichten bis mittelschweren Netzwerk- und Serverlasten. Wie bei jedem Algorithmus, der die Netzwerktransitzeit berücksichtigt, können NTP-Algorithmen unter Bedingungen extremer Netzwerküberlastung schlecht funktionieren. Weitere Informationen zu den NTP-Algorithmen findest du im RFC 1305 in der IETF RFC-Datenbank.

#### <a name="ntp-time-provider"></a>NTP-Zeitanbieter
Der Windows-Zeitdienst ist ein vollständiges Zeitsynchronisierungspaket, das eine Vielzahl von Hardwaregeräten und Zeitprotokollen unterstützen kann. Um diese Unterstützung zu ermöglichen, verwendet der Dienst austauschbare Zeitanbieter. Ein Zeitanbieter ist dafür verantwortlich, entweder genaue Zeitstempel (aus dem Netzwerk oder von der Hardware) abzurufen oder diese Zeitstempel anderen Computern über das Netzwerk bereitzustellen.

Der NTP-Anbieter ist der Standardzeitanbieter, der im Betriebssystem enthalten ist. Der NTP-Anbieter hält die von NTP, Version 3, für einen Client und Server angegebenen Standards ein und kann mit SNTP-Clients und -Servern interagieren, um die Abwärtskompatibilität mit Windows 2000 und anderen SNTP-Clients zu gewährleisten. Der NTP-Anbieter im Windows-Zeitdienst besteht aus den folgenden zwei Teilen:

-   **NtpServer-Ausgabeanbieter**. Dies ist ein Zeitserver, der auf Clientzeitanforderungen im Netzwerk antwortet.

-   **NtpClient-Eingabeanbieter**. Dies ist ein Zeitclient, der Zeitinformationen von einer anderen Quelle (einem Hardwaregerät oder einem NTP-Server) bezieht und Zeitstichproben zurückgeben kann, die für die Synchronisierung der lokalen Uhr nützlich sind.

Obwohl die tatsächlichen Vorgänge dieser beiden Anbieter eng miteinander verknüpft sind, erscheinen sie dem Zeitdienst als unabhängig. Ab Windows 2000 Server wird ein Windows-Computer, wenn er mit einem Netzwerk verbunden ist, als NTP-Client konfiguriert. Außerdem versuchen Computer, auf denen der Windows-Zeitdienst ausgeführt wird, standardmäßig nur, die Zeit mit einem Domänencontroller oder einer manuell angegebenen Zeitquelle zu synchronisieren. Dies sind die bevorzugten Zeitanbieter, weil sie automatisch verfügbare, sichere Zeitquellen sind.

#### <a name="ntp-security"></a>NTP-Sicherheit

Innerhalb einer AD DS-Gesamtstruktur verwendet der Windows-Zeitdienst Standardsicherheitsfunktionen der Domäne, um die Authentifizierung von Zeitdaten zu erzwingen. Die Sicherheit von NTP-Paketen, die zwischen einem Domänenmitgliedscomputer und einem lokalen Domänencontroller gesendet werden, der als Zeitserver fungiert, basiert auf der Authentifizierung über gemeinsam verwendete Schlüssel. Der Windows-Zeitdienst verwendet den Kerberos-Sitzungsschlüssel des Computers, um authentifizierte Signaturen für NTP-Pakete zu erstellen, die über das Netzwerk gesendet werden. NTP-Pakete werden nicht innerhalb des sicheren Kanals der Netzwerkanmeldung übertragen. Stattdessen fordert der Windows-Zeitdienst, wenn ein Computer die Zeit von einem Domänencontroller in der Domänenhierarchie anfordert, dass die Zeit authentifiziert ist. Der Domänencontroller gibt dann die erforderlichen Informationen in Form eines 64-Bit-Werts zurück, der mit dem Sitzungsschlüssel den Netzwerkanmeldediensts authentifiziert wurde. Wenn das zurückgegebene NTP-Paket nicht mit dem Sitzungsschlüssel des Computers signiert oder fehlerhaft signiert wurde, wird die Zeit abgelehnt. Alle solchen Authentifizierungsfehler werden im Ereignisprotokoll protokolliert. Auf diese Weise stellt der Windows-Zeitdienst Sicherheit für NTP-Daten in einer AD DS-Gesamtstruktur her.

Im Allgemeinen rufen Windows-Zeitclients automatisch eine genaue Zeit für die Synchronisierung von Domänencontrollern in derselben Domäne ab. In einer Gesamtstruktur synchronisieren die Domänencontroller einer untergeordneten Domäne die Zeit mit Domänencontrollern in den ihnen übergeordneten Domänen. Wenn ein Zeitserver ein authentifiziertes NTP-Paket an einen Client zurückgibt, der die Zeit anfordert, wird das Paket mithilfe eines Kerberos-Sitzungsschlüssels signiert, der durch ein domänenübergreifendes Vertrauenskonto definiert wird. Das domänenübergreifende Vertrauenskonto wird erstellt, wenn eine neue AD DS-Domäne einer Gesamtstruktur beitritt, und der Netzwerkanmeldedienst verwaltet den Sitzungsschlüssel. Auf diese Weise wird der in der Stammdomäne der Gesamtstruktur als zuverlässig konfigurierte Domänencontroller zur authentifizierten Zeitquelle für alle Domänencontroller in sowohl den übergeordneten als auch den untergeordneten Domänen und indirekt für alle Computer in der Domänenstruktur.

Der Windows-Zeitdienst kann für die Arbeit zwischen Gesamtstrukturen konfiguriert werden, doch es ist wichtig zu beachten, dass diese Konfiguration nicht sicher ist. Beispielsweise kann ein NTP-Server in einer anderen Gesamtstruktur verfügbar sein. Da sich dieser Computer jedoch in einer anderen Gesamtstruktur befindet, gibt es keinen Kerberos-Sitzungsschlüssel, mit dem NTP-Pakete signiert und authentifiziert werden können. Zum Beziehen einer exakten Zeitsynchronisierung von einem Computer in einer anderen Gesamtstruktur benötigt der Client Netzwerkzugriff auf diesen Computer, und der Zeitdienst muss für die Verwendung einer bestimmten Zeitquelle, die sich in der anderen Gesamtstruktur befindet, konfiguriert werden. Wenn ein Client manuell so konfiguriert ist, dass er auf die Zeit von einem NTP-Server außerhalb seiner eigenen Domänenhierarchie zugreift, werden die zwischen dem Client und dem Zeitserver gesendeten NTP-Pakete nicht authentifiziert und sind daher nicht sicher. Selbst bei der Implementierung von Gesamtstruktur-Vertrauensstellungen ist der Windows-Zeitdienst gesamtstrukturübergreifend nicht sicher. Obwohl der sichere Kanal der Netzwerkanmeldung der Authentifizierungsmechanismus für den Windows-Zeitdienst ist, wird eine gesamtstrukturübergreifende Authentifizierung nicht unterstützt.

#### <a name="hardware-devices-that-are-supported-by-the-windows-time-service"></a>Hardwaregeräte, die vom Windows-Zeitdienst unterstützt werden
Hardwarebasierte Uhren, z. B. GPS oder Funkuhren, werden häufig als hochgenaue Referenzuhrgeräte verwendet. Standardmäßig unterstützt der NTP-Zeitanbieter des Windows-Zeitdiensts keine direkte Verbindung eines Hardwaregeräts mit einem Computer, obwohl es möglich ist, einen softwarebasierten unabhängigen Zeitanbieter zu erstellen, der diesen Verbindungstyp unterstützt. Diese Art von Anbieter kann in Verbindung mit dem Windows-Zeitdienst eine zuverlässige, stabile Zeitreferenz bereitstellen.

Hardwaregeräte, z. B. eine Cäsium-Uhr oder ein GPS-Empfänger (Global Positioning System), bieten eine genaue aktuelle Zeit, indem sie einen Standard einhalten, um eine genaue Zeitdefinition zu erhalten. Cäsium-Uhren sind äußerst stabil und sind von Faktoren wie Temperatur, Druck oder Luftfeuchtigkeit unbeeinflusst, sind aber auch sehr teuer. Der Betrieb eines GPS-Empfängers ist wesentlich billiger und stellt außerdem auch eine exakte Referenzuhr dar. GPS-Empfänger erhalten ihre Zeit von Satelliten, die wiederum ihre Zeit von einer Cäsium-Uhr beziehen. Ohne die Verwendung eines unabhängigen Zeitanbieters können Windows-Zeitserver ihre Zeit beziehen, indem sie eine Verbindung mit einem externen NTP-Server herstellen, der über ein Telefon oder das Internet mit einem Hardwaregerät verbunden ist. Organisationen wie das Naval-Observatorium der USA stellen NTP-Server bereit, die mit äußerst zuverlässigen Referenzuhren verbunden sind.

Viele GPS-Empfänger und andere Zeitgeräte können als NTP-Server in einem Netzwerk fungieren. Du kannst deine AD DS-Gesamtstruktur so konfigurieren, dass die Zeit von diesen externen Hardwaregeräten nur dann synchronisiert wird, wenn sie auch als NTP-Server in deinem Netzwerk fungieren. Konfiguriere hierzu den Domänencontroller, der als PDC-Emulator (Primärer Domänencontroller) im Stamm deiner Gesamtstruktur fungiert, so, dass er mit dem von dem GPS-Gerät bereitgestellten NTP-Server synchronisiert. Informationen zur Vorgehensweise hierfür findest du unter [Konfigurieren des Windows-Zeitdiensts im PDC-Emulator in der Stammdomäne der Gesamtstruktur](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29).

### <a name="simple-network-time-protocol"></a>Simple Network Time Protocol (SNTP)
Das Simple Network Time Protocol (SNTP) ist ein vereinfachtes Zeitprotokoll, das für Server und Clients vorgesehen ist, die nicht auf den Genauigkeitsgrad angewiesen sind, der von NTP bereitgestellt wird. SNTP, eine rudimentärere Version von NTP, ist das primäre Zeitprotokoll, das in Windows 2000 verwendet wird. Da die Netzwerkpaketformate von SNTP und NTP identisch sind, sind die beiden Protokolle interoperabel. Der Hauptunterschied zwischen den beiden besteht darin, dass SNTP nicht über die Fehlerverwaltungs- und komplexen Filtersysteme verfügt, die NTP bereitstellt. Weitere Informationen zum Simple Network Time Protocol findest du im RFC 1769 in der IETF RFC-Datenbank.

### <a name="time-protocol-interoperability"></a>Interoperabilität von Zeitprotokollen
Der Windows-Zeitdienst kann in einer gemischten Umgebung mit Computern unter Windows 2000, Windows XP und Windows Server 2003 ausgeführt werden, da das in Windows 2000 verwendete SNTP-Protokoll mit dem NTP-Protokoll in Windows XP und Windows Server 2003 interoperabel ist.

Der Zeitdienst in Windows NT Server 4.0, namens TimeServ, synchronisiert die Zeit in einem Windows NT 4.0-Netzwerk. TimeServ ist eine Add-On-Funktion, die als Teil des *Microsoft Windows NT 4.0 Resource Kits* verfügbar ist und nicht den Grad an Zuverlässigkeit der Zeitsynchronisierung bietet, der von Windows Server 2003 benötigt wird.

Der Windows-Zeitdienst kann mit Computern interagieren, auf denen Windows NT 4.0 ausgeführt wird, weil diese Zeit mit Computern mit Windows 2000 oder Windows Server 2003 synchronisieren können. Ein Computer mit Windows 2000 oder Windows Server 2003 ermittelt jedoch nicht automatisch Windows NT 4.0-Zeitserver. Wenn deine Domäne beispielsweise so konfiguriert ist, dass die Zeit mithilfe der domänenhierarchiebasierten Synchronisierungsmethode synchronisiert wird, und deine Computer in der Domänenhierarchie die Zeit mit einem Windows NT 4.0-Domänencontroller synchronisieren sollen, musst du diese Computer manuell so konfigurieren, dass sich mit den Windows NT 4.0-Domänencontrollern synchronisieren.

Windows NT 4.0 verwendet einen einfacheren Mechanismus für die Zeitsynchronisierung als der Windows-Zeitdienst. Um eine genaue Zeitsynchronisierung im Netzwerk sicherzustellen, empfiehlt es sich daher, ein Upgrade aller Windows NT 4.0-Domänencontroller auf Windows 2000 oder Windows Server 2003 vorzunehmen.

## <a name="windows-time-service-processes-and-interactions"></a>Windows-Zeitdienst: Prozesse und Interaktionen

Der Windows-Zeitdienst ist so konzipiert, dass die Uhren von Computern in einem Netzwerk synchronisiert werden. Der Prozess der Zeitsynchronisierung im Netzwerk (auch „Zeitkonvergenz“ genannt) tritt im gesamten Netzwerk auf, wenn jeder Computer auf die Zeit von einem präziseren Zeitserver zugreift. Zeitkonvergenz umfasst einen Prozess, durch den ein autoritativer Server den Clientcomputern die aktuelle Zeit in Form von NTP-Paketen bereitstellt. Die in einem Paket enthaltenen Informationen geben an, ob eine Anpassung der aktuellen Uhrzeit des Computers vorgenommen werden muss, damit sie mit dem genaueren Server synchronisiert wird.

Im Rahmen des Zeitkonvergenzprozesses versuchen Domänenmitglieder, die Zeit mit einem beliebigen Domänencontroller in derselben Domäne zu synchronisieren. Wenn der Computer ein Domänencontroller ist, versucht er, sich mit einem autoritativerem Domänencontroller zu synchronisieren.

Computer, auf denen Windows XP Home Edition ausgeführt wird, oder Computer, die keiner Domäne beigetreten sind, versuchen nicht, sich mit der Domänenhierarchie zu synchronisieren, sondern sind standardmäßig so konfiguriert, dass sie die Zeit von „time.windows.com“ beziehen.

Um einem Computer, auf dem Windows Server 2003 ausgeführt wird, den Status „autoritativ“ zu verschaffen, muss der Computer als zuverlässige Zeitquelle konfiguriert sein. Standardmäßig wird der erste Domänencontroller, der in einer Windows Server 2003-Domäne installiert ist, automatisch als zuverlässige Zeitquelle konfiguriert. Da es sich um den autoritativen Computer für die Domäne handelt, muss er so konfiguriert werden, dass er sich mit einer externen Zeitquelle und nicht mit der Domänenhierarchie synchronisiert. Ebenfalls standardmäßig werden alle anderen Windows Server 2003-Domänenmitglieder so konfiguriert, dass sie sich mit der Domänenhierarchie synchronisieren.

Nachdem du ein Windows Server 2003-Netzwerk eingerichtet hast, kannst du den Windows-Zeitdienst so konfigurieren, dass eine der folgenden Optionen für die Synchronisierung verwendet wird:

-   Synchronisierung auf Basis der Domänenhierarchie

-   Eine manuell angegebene Synchronisierungsquelle

-   Alle verfügbaren Synchronisierungsmechanismen

-   Keine Synchronisierung.

Jede dieser Synchronisierungsarten wird im folgenden Abschnitten einzeln behandelt.

### <a name="domain-hierarchy-based-synchronization"></a>Synchronisierung auf Basis der Domänenhierarchie

Die Synchronisierung auf Grundlage der Domänenhierarchie verwendet die AD DS-Domänenhierarchie, um eine zuverlässige Quelle zu finden, mit der die Zeit synchronisiert werden soll. Basierend auf der Domänenhierarchie bestimmt der Windows-Zeitdienst die Genauigkeit jedes Zeitservers. In einer Windows Server 2003-Gesamtstruktur hat der Computer, der die Betriebsmasterrolle des PDC-Emulators (primärer Domänencontroller) in der Stammdomäne besitzt, die Position der besten Zeitquelle inne, es sei denn, eine andere zuverlässige Zeitquelle wurde konfiguriert. In der folgenden Abbildung wird ein Pfad zur Zeitsynchronisierung zwischen Computern in einer Domänenhierarchie veranschaulicht.

**Zeitsynchronisierung in einer AD DS-Hierarchie**
![Windows-Zeit](../media/Windows-Time-Service/How-the-Windows-Time-Service-Works/trnt_ntw_adhc.gif)

#### <a name="reliable-time-source-configuration"></a>Konfiguration einer zuverlässigen Zeitquelle
Ein Computer, der als zuverlässige Zeitquelle konfiguriert ist, wird als Stamm des Zeitdiensts identifiziert. Der Stamm des Zeitdiensts ist der autoritative Server für die Domäne und wird in der Regel so konfiguriert, dass er die Zeit von einem externen NTP-Server oder einem Hardwaregerät bezieht. Ein Zeitserver kann als zuverlässige Zeitquelle konfiguriert werden, um zu optimieren, wie die Zeit in der gesamten Domänenhierarchie übertragen wird. Wenn ein Domänencontroller als zuverlässige Zeit Quelle konfiguriert ist, kündigt der Netzwerkanmeldedienst diesen Domänencontroller als zuverlässige Zeitquelle an, wenn die Anmeldung am Netzwerk erfolgt. Wenn andere Domänencontroller nach einer Zeitquelle suchen, um sich damit zu synchronisieren, wählen sie als Erstes eine zuverlässige Quelle aus, sofern eine verfügbar ist.

#### <a name="time-source-selection"></a>Auswahl der Zeitquelle
Der Vorgang zur Auswahl der Zeitquelle kann zwei Probleme in einem Netzwerk verursachen:

-   Zusätzliche Synchronisierungszyklen.

-   Höheres Volumen beim Netzwerkdatenverkehr.

Ein Synchronisierungszyklus im Netzwerk tritt auf, wenn die Zeit zwischen einer Gruppe von Domänencontrollern konsistent bleibt und dieselbe Zeit fortlaufend von diesen gemeinsam genutzt wird, ohne sich mit einer anderen zuverlässigen Zeitquelle erneut zu synchronisieren. Die Auswahl der Zeitquelle durch den Windows-Zeitdienst ist darauf ausgelegt, vor Problemen dieser Arten zu schützen.

Ein Computer verwendet eine der folgenden Methoden, um eine Zeitquelle für die Synchronisierung zu identifizieren:

-   Wenn der Computer kein Mitglied einer Domäne ist, muss er so konfiguriert werden, dass er sich mit einer angegebenen Zeitquelle synchronisiert.

-   Wenn der Computer ein Mitgliedsserver oder eine Arbeitsstation in einer Domäne ist, durchläuft er standardmäßig die AD DS-Hierarchie und synchronisiert seine Zeit mit einem Domänencontroller in seiner lokalen Domäne, auf dem derzeit der Windows-Zeitdienst ausgeführt wird.

Wenn der Computer ein Domänencontroller ist, führt er bis zu 6 Abfragen aus, um einen anderen Domänencontroller zu finden, um sich mit diesem zu synchronisieren. Jede Abfrage ist so konzipiert, dass sie eine Zeitquelle mit bestimmten Attributen identifiziert, z. B. ein Typ von Domänencontroller, ein bestimmter Standort, und ob es sich um eine zuverlässige Zeitquelle handelt oder nicht. Die Zeitquelle muss außerdem die folgenden Einschränkungen einhalten:

-   Eine zuverlässige Zeitquelle kann sich nur mit einem Domänencontroller in der übergeordneten Domäne synchronisieren.

-   Ein PDC-Emulator kann sich mit einer zuverlässigen Zeitquelle in seiner eigenen Domäne oder mit einem beliebigen Domänencontroller in der übergeordneten Domäne synchronisieren.

Wenn sich der Domänencontroller nicht mit dem Typ von Domänencontroller synchronisieren kann, den er abgefragt, wird die Abfrage nicht durchgeführt. Der Domänencontroller weiß, von welchem Computertyp er die Zeit beziehen kann, bevor er die Abfrage ausführt. Beispielsweise versucht ein lokaler PDC-Emulator nicht, Nr. 3 oder 6 abzufragen, weil ein Domänencontroller nicht versucht, sich mit sich selbst zu synchronisieren.

In der folgenden Tabelle sind die Abfragen aufgelistet, die von einem Domänencontroller gestellt werden, um eine Zeitquelle aufzufinden, sowie die Reihenfolge, in der die Abfragen gestellt werden.

**Zeitquellenabfragen eines Domänencontrollers**

|Abfragenummer|Domänencontroller|Speicherort|Zuverlässigkeit der Zeitquelle|
|----------------|---------------------|------------|------------------------------|
|1|Übergeordneter Domänencontroller|Standortintern|Bevorzugt eine zuverlässige Zeitquelle, kann sich aber mit einer nicht zuverlässigen Zeitquelle synchronisieren, wenn nichts anderes verfügbar ist.|
|2|Lokaler Domänencontroller|Standortintern|Synchronisiert sich nur mit einer zuverlässigen Zeitquelle.|
|3|Lokaler PDC-Emulator|Standortintern|Nicht anwendbar.<p>Ein Domänencontroller versucht nicht, sich mit sich selbst zu synchronisieren.|
|4|Übergeordneter Domänencontroller|Außerhalb des Standorts|Bevorzugt eine zuverlässige Zeitquelle, kann sich aber mit einer nicht zuverlässigen Zeitquelle synchronisieren, wenn nichts anderes verfügbar ist.|
|5|Lokaler Domänencontroller|Außerhalb des Standorts|Synchronisiert sich nur mit einer zuverlässigen Zeitquelle.|
|6|Lokaler PDC-Emulator|Außerhalb des Standorts|Nicht anwendbar.<p>Ein Domänencontroller versucht nicht, sich mit sich selbst zu synchronisieren.|

**Hinweis**

-   Ein Computer synchronisiert sich niemals mit sich selbst. Wenn der Computer, der die Synchronisierung versucht, der lokale PDC-Emulator ist, versucht er weder Abfrage 3 noch 6.

Jede Abfrage gibt eine Liste von Domänencontrollern zurück, die als Zeitquelle verwendet werden können. Der Windows-Zeitdienst weist jedem Domänencontroller, der abgefragt wird, eine Bewertung zu, basierend auf der Zuverlässigkeit und dem Standort des Domänencontrollers. In der folgenden Tabelle werden die Bewertungen aufgeführt, die jedem Typ von Domänencontroller vom Windows-Zeitdienst zugewiesen werden.

**Ermittlung der Bewertung**

|Status des Domänencontrollers|Bewertung|
|----------------------------|---------|
|Domänencontroller befindet sich am selben Standort.|8|
|Domänencontroller als zuverlässige Zeitquelle gekennzeichnet.|4|
|Domänencontroller befindet sich in der übergeordneten Domäne.|2|
|Domänencontroller, der ein PDC-Emulator ist.|1|

Wenn der Windows-Zeitdienst feststellt, dass er den Domänencontroller mit der bestmöglichen Bewertung identifiziert hat, werden keine weiteren Abfragen mehr durchgeführt. Die vom Zeitdienst zugewiesenen Bewertungen sind kumulativ, was bedeutet, dass ein PDC-Emulator, der sich am selben Standort befindet, eine Bewertung von 9 erhält.

Wenn der Stamm des Zeitdiensts nicht für die Synchronisierung mit einer externen Quelle konfiguriert ist, regelt die interne Hardwareuhr des Computers die Zeit.

### <a name="manually-specified-synchronization"></a>Manuell angegebene Synchronisierung
Mithilfe der manuell angegebenen Synchronisierung kannst du einen einzelnen Peer oder eine Liste von Peers bestimmen, von denen ein Computer seine Zeit beziehen soll. Wenn der Computer kein Mitglied einer Domäne ist, muss er manuell so konfiguriert werden, dass er sich mit einer angegebenen Zeitquelle synchronisiert. Ein Computer, der Mitglied einer Domäne ist, wird standardmäßig für die Synchronisierung aus der Domänenhierarchie konfiguriert. Die manuell angegebene Synchronisierung ist am nützlichsten für den Gesamtstrukturstamm der Domäne oder für Computer, die keiner Domäne beigetreten sind. Das manuelle Angeben eines externen NTP-Servers für die Synchronisierung mit dem autoritativen Computer für deine Domäne sorgt für eine zuverlässige Zeit. Das Konfigurieren des autoritativen Computers für deine Domäne zur Synchronisierung mit einer Hardwareuhr ist tatsächlich eine bessere Lösung für die Bereitstellung der genauesten und sicheren Zeit in deiner Domäne.

Manuell angegebene Zeitquellen werden nicht authentifiziert, es sei denn, ein bestimmter Zeitanbieter wurde für sie geschrieben, weshalb Sie für Angreifer anfällig sind. Auch wenn ein Computer sich mit einer manuell angegebenen Quelle synchronisiert, anstatt mit seinem authentifizierenden Domänencontroller, kann es sein, dass die beiden Computer nicht mehr synchronisiert sind, was zum Fehlschlagen der Kerberos-Authentifizierung führt. Dies wiederum kann dazu führen, dass andere Aktionen, die eine Netzwerkauthentifizierung erfordern, fehlschlagen, beispielsweise Drucken oder Teilen einer Datei. Wenn nur der Gesamtstrukturstamm für die Synchronisierung mit einer externen Quelle konfiguriert ist, bleiben alle anderen Computer innerhalb der Gesamtstruktur miteinander synchronisiert, was Replay-Angriffe erschwert.

### <a name="all-available-synchronization-mechanisms"></a>Alle verfügbaren Synchronisierungsmechanismen

Die Option „Alle verfügbaren Synchronisierungsmechanismen“ ist die wertvollste Synchronisierungsmethode für Benutzer in einem Netzwerk. Diese Methode ermöglicht die Synchronisierung mit der Domänenhierarchie und kann außerdem, abhängig von der Konfiguration, eine alternative Zeitquelle bieten, wenn die Domänenhierarchie nicht mehr verfügbar ist. Wenn der Client seine Zeit nicht mit der Domänenhierarchie synchronisieren kann, wird automatisch ein Fallback für die Zeitquelle auf die über die Einstellung **NtpServer** angegeben Zeitquelle durchgeführt. Diese Synchronisierungsmethode bietet mit höchster Wahrscheinlich eine genaue Zeit für Clients.

### <a name="stopping-time-synchronization"></a>Beenden der Zeitsynchronisierung
Es gibt bestimmte Situationen, in denen du verhindern möchtest, dass ein Computer seine Zeit synchronisiert. Beispielsweise wenn ein Computer versucht, sich mit einer Zeitquelle im Internet oder einer Zeitquelle an einem anderen Standort mittels DFÜ-Verbindung über ein WAN zu synchronisieren, kann dies kostspielige Telefongebühren verursachen. Wenn du die Synchronisierung auf diesem Computer deaktivierst, verhinderst du, dass der Computer über eine DFÜ-Verbindung auf eine Zeitquelle zugreift.

Du kannst die Synchronisierung auch deaktivieren, um die Generierung von Fehlern im Ereignisprotokoll zu verhindern. Jedes Mal, wenn ein Computer versucht, sich mit einer nicht verfügbaren Zeitquelle zu synchronisieren, generiert er einen Fehler im Ereignisprotokoll. Wenn eine Zeitquelle für eine geplante Wartung vom Netz genommen wird, und du nicht beabsichtigst, den Client so neu zu konfigurieren, dass er sich mit einer anderen Quelle synchronisiert, kannst du die Synchronisierung auf dem Client deaktivieren, um zu verhindern, dass er eine Synchronisierung versucht, solange der Zeitserver nicht verfügbar ist.

Es ist hilfreich, die Synchronisierung auf dem Computer zu deaktivieren, der als Stamm des Synchronisierungsnetzwerks festgelegt ist. Dies gibt an, dass der Stammcomputer seiner lokalen Uhr vertraut. Wenn der Stamm der Synchronisierungshierarchie nicht auf **NoSync** festgelegt ist, und er sich nicht mit einer anderen Zeitquelle synchronisieren kann, akzeptieren Clients das Paket nicht, das dieser sendet, weil seine Zeit nicht vertrauenswürdig ist.

Die einzigen Zeitserver, denen Clients auch dann vertrauen, wenn sie nicht mit einer anderen Zeitquelle synchronisiert wurden, sind solche, die vom Client als zuverlässige Zeitserver identifiziert wurden.

### <a name="disabling-the-windows-time-service"></a>Deaktivieren des Windows-Zeitdiensts
Der Windows-Zeitdienst (W32Time) kann vollständig deaktiviert werden. Wenn du dich entschließt, das Produkt eines Drittanbieters für die Zeitsynchronisierung zu implementieren, das NTP verwendet, musst du den Windows-Zeitdienst deaktivieren. Der Grund hierfür ist, dass alle NTP-Server Zugriff auf den UDP-Port 123 (User Datagram Protocol) benötigen, und dass, solange der Windows-Zeitdienst unter dem Betriebssystem Windows Server 2003 ausgeführt wird, der Port 123 für den Windows-Zeitdienst reserviert bleibt.

## <a name="network-ports-used-by-windows-time-service"></a>Vom Windows-Zeitdienst verwendete Netzwerkports
Der Windows-Zeitdienst kommuniziert in einem Netzwerk, um zuverlässige Zeitquellen zu ermitteln, Zeitinformationen zu beziehen und anderen Computern Zeitinformationen bereitzustellen. Er führt diese Kommunikation wie in den RFCs zu NTP und SNTP definiert durch.

**Portzuweisungen für den Windows-Zeitdienst**

|Dienstname|UDP|TCP|
|----------------|-------|-------|
|NTP|123|NICHT ZUTREFFEND|
|SNTP|123|NICHT ZUTREFFEND|

## <a name="see-also"></a>Weitere Informationen
[Technische Referenz zum Windows-Zeitdienst](windows-time-service-tech-ref.md)
[Windows-Zeitdienst: Tools und Einstellungen](Windows-Time-Service-Tools-and-Settings.md)
[Microsoft Knowledge Base-Artikel 902229](https://go.microsoft.com/fwlink/?LinkId=186066)