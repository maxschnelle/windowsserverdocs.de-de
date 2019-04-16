---
ms.assetid: d1953097-63ea-4a0e-b860-2f3b7c175c41
title: Wie funktioniert der Windows-Zeitdienst
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: c9ab52229c2a16d6ae6b0b2733c52e53a25cfa44
ms.sourcegitcommit: fb4e2ace2e0a29e0f6b028f1cb945cab6aa6ee2c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/05/2018
---
# <a name="how-the-windows-time-service-works"></a>Wie funktioniert der Windows-Zeitdienst

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

**In diesem Abschnitt**  
  
-   [Windows-Zeitdienst-Architektur](#w2k3tr_times_how_rrfo)  
  
-   [Windows Time Service-Zeit-Protokolle](#w2k3tr_times_how_ekoc)  
  
-   [Windows Time Serviceprozesse und-Interaktionen](#w2k3tr_times_how_izcr)  
  
-   [Netzwerk-Ports, die von Windows-Zeitdienst verwendet](#w2k3tr_times_how_ydum)  
  
> [!NOTE]  
> In diesem Thema wird erläutert, wie nur die Windows-Zeitdienst (W32Time) funktioniert. Informationen zum Konfigurieren der Windows-Zeitdienst finden Sie in der Liste der Themen im Abschnitt [, wo Sie Windows Time Service-Konfigurationsinformationen finden](https://technet.microsoft.com/library/cc773061.aspx).  
  
> [!NOTE]  
> In Windows Server 2003 und Microsoft Windows 2000 Server heißt der Verzeichnisdienst Active Directory-Dienst. In Windows Server 2008 und höhere Versionen heißt der Verzeichnisdienst Active Directory-Domänendienste (AD DS). Im weiteren Verlauf dieses Themas bezieht sich auf AD DS, aber die Informationen gilt auch für Active Directory.  
  
Windows-Zeitdienst ist, zwar keine genaue Implementierung von der Netzwerkzeitprotokoll (NTP) verwendet er die komplexe Suite von Algorithmen, die in den NTP-Spezifikationen, um sicherzustellen, dass die Uhren auf mehreren Computern in einem Netzwerk so genau wie möglich definiert ist. Im Idealfall werden alle Computeruhren in AD DS-Domäne mit der Zeit von einem autorisierenden Computer synchronisiert. Die zeitsynchronisierung in einem Netzwerk können von vielen Faktoren beeinflusst. Folgende Faktoren spielen häufig die Genauigkeit der in AD DS-Synchronisierung:  
  
-   Netzwerkbedingungen  
  
-   Die Genauigkeit der Hardware-Uhr des Computers  
  
-   Die Menge an CPU und Netzwerk verfügbaren Ressourcen für Windows-Zeitdienst  
  
> [!IMPORTANT]  
> Vor Windows Server 2016 wurde der W32Time-Dienst nicht für zeitabhängige Anwendung Anforderungen entwickelt.  Updates für Windows Server 2016 jetzt können Sie jedoch zum Implementieren einer Lösung für 1ms Genauigkeit in Ihrer Domäne.  Weitere Informationen finden Sie unter [Windows 2016 genau Zeit](accurate-time.md) und [Unterstützung Grenze so konfigurieren Sie die Windows-Zeitdienst für Umgebungen mit hoher Genauigkeit](https://go.microsoft.com/fwlink/?LinkID=179459) Weitere Informationen.  
  
Computer, die synchronisieren ihre Zeit weniger häufig oder sind nicht Mitglied einer Domäne, sind standardmäßig zum Synchronisieren mit time.windows.com konfiguriert. Daher ist es unmöglich, zeitgenauigkeit auf Computern, die zeitweilig oder keine Netzwerkverbindungen zu gewährleisten.  
  
Eine AD DS-Gesamtstruktur verfügt über eine vorher festgelegten Zeit Synchronisierung-Hierarchie. Windows-Zeitdienst synchronisiert die Uhrzeit zwischen Computern innerhalb der Hierarchie mit den genauesten Verweis Uhren oben. Wenn mehr als eine Zeitquelle auf einem Computer konfiguriert ist, verwendet Windows-Zeitdienst NTP-Algorithmen, um die beste Zeitquelle von der konfigurierten Quelle, die basierend auf dem Computer können Sie mit diesem Zeitquelle synchronisieren auszuwählen. Windows-Zeitdienst wird nicht Netzwerk Synchronisierung von Broadcast oder multicast Peers unterstützt. Weitere Informationen zu diesen NTP-Features finden Sie unter RFC 1305 in der IETF RFC-Datenbank.  
  
Jeder Computer mit der Windows-Zeitdienst verwendet der Dienst die genauesten geplant. Computer, die Mitglied einer Domäne sind fungieren als Zeit Client standardmäßig, daher, in den meisten Fällen ist es nicht erforderlich, um den Windows-Zeitdienst konfigurieren. Der Windows-Zeitdienst kann konfiguriert werden, um eine festgelegte Referenz Zeitquelle Zeit anfordern und können auch Zeit für Clients bereitstellen.
  
Die Zeit des Computers genau ist, wird eine Schicht aufgerufen. Die genaueste Zeitquelle in einem Netzwerk (z. B. eine Hardware-Uhr) nimmt die unterste Schicht-Ebene oder eine Schicht. Diese Zeitquelle wird eine Referenzuhr aufgerufen. Ein NTP-Server, der direkt von einer Uhr Verweis Zeit erhält belegt ist eine Schicht, die eine Ebene höher als die der Uhr Verweis ist. Ressourcen, die vom NTP-Server abrufen sind zwei Schritte der Referenzuhr und daher eine Schicht, die zwei ist höher als die genauesten Zeitquelle belegen, usw. Anzahl von einem Computer Schicht zunimmt, die Zeit der Systemuhr möglicherweise weniger präzise. Daher ist die Schicht auf jedem Computer ein Indikator für die Übereinstimmung zwischen diesem Computer mit den genauesten Zeitquelle synchronisiert wird.  
  
Wenn der W32Time-Manager Stichproben erhält, verwendet er spezielle Algorithmen in NTP um zu ermitteln, die von den Stichproben am besten geeignet für die Verwendung. Der Zeitdienst verwendet auch einen anderen Satz von Algorithmen um zu ermitteln, welche die konfigurierte Zeitquellen am präzisesten angezeigt. Wenn der Zeitdienst ermittelt hat, welche Uhrzeit Beispiel am besten geeignet ist, wird angepasst anhand der oben genannten Kriterien, der lokalen Taktfrequenz, um auf die richtige Zeit konvergieren zulassen. Wenn der Zeitunterschied zwischen lokaler Uhrzeit und die ausgewählten genaue Uhrzeit (auch als die Zeit Zeitversatz) zu beheben, indem Sie der lokalen Taktfrequenz groß ist, wird der Zeitdienst lokalen Uhrzeit auf die richtige Uhrzeit festgelegt. Diese Anpassung Taktfrequenz oder direkten uhrzeitänderung wird als Uhr Disziplin bezeichnet.  
  
## <a name="w2k3tr_times_how_rrfo"></a>Windows-Zeitdienst-Architektur  
Windows-Zeitdienst besteht aus den folgenden Komponenten:  
  
-   Dienststeuerungs-Manager  
  
-   Windows Time Service Manager  
  
-   Uhr Disziplin  
  
-   Zeitanbieter  
  
Die folgende Abbildung zeigt die Architektur der Windows-Zeitdienst.  
  
**Windows-Zeitdienst-Architektur**  
  
![Windows-Zeitdienst](media/How-the-Windows-Time-Service-Works/trnt_sec_arcc.gif)  
  
Dienststeuerungs-Manager ist verantwortlich für das Starten und Beenden von Windows-Zeitdienst. Die Windows Time Service Manager ist verantwortlich für das Starten der Aktion NTP Zeitanbieter mit dem Betriebssystem enthalten. Die Windows Time Service Manager steuert alle Funktionen der Windows-Zeitdienst und die Zusammenfügung aller Zeit Beispiele. Zusätzlich zu bieten Informationen zu den aktuellen Systemstatus, z. B. die aktuelle Zeitquelle oder der letzten Zeit die Systemuhr aktualisiert wurde, ist die Windows Time Service Manager auch verantwortlich für das Erstellen von Ereignissen im Ereignisprotokoll.  
  
Der Synchronisierungsprozess Zeit umfasst die folgenden Schritte aus:  
  
-   Eingabe Anbieter anfordern und Stichproben von konfigurierten NTP-Zeitquellen erhalten.  
  
-   Diese Beispiele Zeit werden dann zu Windows Time Service Manager übergeben, die alle Beispiele erfasst und übergibt sie an die Uhr Disziplin Unterkomponente.  
  
-   Die Uhr Disziplin Unterkomponente gilt der NTP-Algorithmen, die in der Auswahl des besten Zeit Beispiels führt.  
  
-   Die Uhr Disziplin Unterkomponente passt die Zeit der Systemuhr auf die genauesten Zeit durch Anpassen der Taktfrequenz oder direkt zu die Zeit ändern.  
  
Wenn ein Computer als einen Server festgelegt wurde, können sie die Zeit an einem beliebigen Computer anfordern Synchronisierung zu jedem beliebigen Zeitpunkt in diesem Prozess senden.  
  
## <a name="w2k3tr_times_how_ekoc"></a>Windows Time Service-Zeit-Protokolle  

Zeit Protokolle zu bestimmen, wie genau zwei Computern Uhren synchronisiert werden. Ein Protokoll Zeit ist verantwortlich für bestimmen die beste verfügbare Informationen und konvergierender die Uhren, um sicherzustellen, dass eine einheitliche Zeit in getrennten Systemen verwaltet wird.  
  
Windows-Zeitdienst verwendet das Netzwerkzeitprotokoll (NTP), um die Zeit in einem Netzwerk zu synchronisieren. NTP ist ein Internet-Zeit-Protokoll, das die Disziplin Algorithmen für die Synchronisierung von Uhren erforderlichen enthält. NTP ist eine genauere NTP als SNTP Simple Network Time Protocol (), die in einigen Versionen von Windows verwendet wird. Allerdings unterstützt auch weiterhin W32Time SNTP um Abwärtskompatibilität mit Zeit SNTP-basierte Dienste, z. B. Windows 2000-Computern zu aktivieren.  
  
### <a name="network-time-protocol"></a>Network Time Protocol  
Netzwerkzeitprotokoll (NTP) ist die Standardeinstellung Zeit Synchronisierungsprotokoll, das vom Windows-Zeitdienst im Betriebssystem. NTP ist ein Protokoll fehlertolerante, hoch skalierbare Zeit und das Protokoll für die Synchronisierung von Computeruhren mithilfe eines Verweises festgelegten Zeit am häufigsten verwendet.  
  
NTP Synchronisierung erfolgt über einen gewissen Zeitraum und die Übertragung von NTP-Pakete über ein Netzwerk umfasst. NTP-Pakete enthalten, die eine Zeit Beispiel aus der Client- und der teilnehmenden zeitlich enthalten.  
  
NTP stützt sich auf eine Referenzuhr zum Definieren des genauesten verwendet werden und alle Uhren in einem Netzwerk dieser Referenz Uhr synchronisiert. NTP verwendet koordinierte Weltzeit (UTC) als universelle Standard für die aktuelle Zeit. UTC-Zeit ist unabhängig von Zeitzonen und NTP an einer beliebigen Stelle in der ganzen Welt, unabhängig von der zeitzoneneinstellungen verwendet werden kann.  
  
#### <a name="ntp-algorithms"></a>NTP-Algorithmen  
NTP enthält zwei Algorithmen, einen Algorithmus Uhr-Filterung und eine Uhr Auswahl-Algorithmus, um Windows-Zeitdienst ermitteln die beste Zeit Beispiel. Der Algorithmus Uhr-Filter Dient zum durchsucht Stichproben werden müssen, die von abgefragten Zeitquellen empfangen werden, und ermitteln die beste Zeit Beispiele aus jeder Quelle. Die Uhr Auswahl Algorithmus bestimmt den genauesten Zeitserver im Netzwerk. Diese Informationen werden dann des Algorithmus Uhr Disziplin übergeben, die erfassten Daten verwendet in der lokalen Zeit des Computers, zu beheben, und Fehler aufgrund von Netzwerk Latenz und Computer Uhr wesentlich ungenauer als kompensieren.  
  
Die NTP-Algorithmen sind unter Umständen Licht "Mittel" Netzwerk- und Lasten am präzisesten angezeigt. Wie bei allen Algorithmus, der während der Übertragung Netzwerkzeit berücksichtigt, möglicherweise NTP-Algorithmen unter Umständen Überlastung des Netzwerks extreme nur mit schlechter Leistung führen. Weitere Informationen zu den NTP-Algorithmen finden Sie unter RFC 1305 in der IETF RFC-Datenbank.  
  
#### <a name="ntp-time-provider"></a>NTP-Zeitanbieter  
Windows-Zeitdienst ist eine vollständige Uhrzeit Synchronisierung-Paket, die eine Vielzahl von Hardwaregeräten und Zeit Protokolle unterstützen kann. Um diese Unterstützung zu aktivieren, verwendet der Dienst austauschbare Zeitanbieter. Ein Zeitanbieter ist verantwortlich für entweder abrufen genaue Zeitstempel (über das Netzwerk oder von der Hardware) oder für die Bereitstellung dieser Zeitstempel auf andere Computer über das Netzwerk.  
  
Der NTP-Anbieter ist die Standardzeit-Anbieter, die mit dem Betriebssystem enthalten. Der NTP-Anbieter folgt den Standards NTP Version 3 für einen Client und Server angegeben, und SNTP-Clients und-Server für die Abwärtskompatibilität mit Windows 2000 und anderen SNTP-Clients interagieren kann. Der NTP-Anbieter in der Windows-Zeitdienst besteht aus den folgenden zwei Teilen:  
  
-   **NtpServer Ausgabe-Anbieter.** Dies ist ein Zeitserver aus, der auf Zeit Clientanforderungen im Netzwerk reagiert.  
  
-   **NtpClient input-Anbieter.** Dies ist ein Mal-Client, der Informationen aus einer anderen Quelle, ein Gerät oder einem NTP-Server abgerufen und Stichproben, die für die Synchronisierung der lokalen Uhr zurückgeben kann.  
  
Obwohl die tatsächliche Vorgänge dieser zwei Anbieter eng miteinander verbunden sind, werden diese auf den Zeitdienst unabhängig. Ab Windows 2000 Server, bei ein Windows-Computer mit einem Netzwerk verbunden ist, wird er als NTP-Client konfiguriert. Computer mit der Windows-Zeitdienst service auch nur Versuch Zeit standardmäßig mit einem Domänencontroller oder einem manuell angegebene Zeitquelle synchronisieren. Diese sind der bevorzugte Zeitanbieter, da sie automatisch zur Verfügung, sicheren Quellen Zeit sind.  
  
#### <a name="ntp-security"></a>NTP-Sicherheit  

In einer AD DS-Gesamtstruktur verwendet der Windows-Zeitdienst standard-Domäne Sicherheitsfeatures, die Authentifizierung von Entwurfszeitdaten zu erzwingen. Die Sicherheit des NTP-Pakete, die zwischen einem Domänenmitgliedscomputer und einen lokalen Domänencontroller, der als ein Server Authentifizierung basiert fungiert, gesendet werden. Windows-Zeitdienst verwendet der Computer Kerberos-Sitzungsschlüssel authentifizierte Signaturen auf NTP-Pakete erstellen, die über das Netzwerk gesendet werden. NTP-Pakete werden nicht in den Anmeldedienst sicheren Kanal übertragen. Stattdessen, wenn ein Computer die Zeit von einem Domänencontroller in der Domänenhierarchie anfordert, muss der Windows-Zeitdienst die Zeit authentifiziert werden. Der Domänencontroller gibt dann die erforderliche Informationen in Form von einem 64-Bit-Wert, der mit dem Sitzungsschlüssel aus der Netlogon-Dienst authentifiziert wurde. Wenn das zurückgegebene NTP-Paket nicht mit dem Computer Sitzungsschlüssel signiert ist oder nicht ordnungsgemäß signiert ist, wird die Zeit abgelehnt. Solche Authentifizierungsfehler werden im Ereignisprotokoll protokolliert. Auf diese Weise bietet der Windows-Zeitdienst Sicherheit für NTP-Daten in einer AD DS-Gesamtstruktur.  
  
In der Regel, erhalten Clients der Windows-Zeit automatisch genaue Uhrzeit für die Synchronisierung von Domänencontrollern in der gleichen Domäne. In einer Gesamtstruktur synchronisieren Sie die Domänencontroller einer untergeordneten Domäne Zeit mit Domänencontrollern in Domänen. Wenn Sie ein Server ein authentifizierter NTP-Paket an einen Client zurückgegeben, die die Zeit anfordert, wird das Paket durch ein Kerberos-Sitzungsschlüssel durch eine Vertrauenskonto definiert signiert. Die Vertrauenskonto wird erstellt, wenn eine neue AD DS-Domäne hinzugefügt, einer Gesamtstruktur wird und der Netlogon-Dienst den Sitzungsschlüssel verwaltet. Auf diese Weise wird der Domänencontroller, der in der Gesamtstruktur-Stammdomäne als zuverlässig konfiguriert ist den authentifizierten Zeitquelle für alle Domänencontroller in der übergeordneten und untergeordneten Domänen und indirekt für alle Computer in der Struktur von Domäne.  
  
Windows-Zeitdienst kann so konfiguriert werden, dass zwischen Gesamtstrukturen möglich, aber es ist wichtig zu beachten, dass diese Konfiguration nicht sicher ist. Ein NTP-Server kann beispielsweise in einer anderen Gesamtstruktur verfügbar sein. Da dieser Computer in einer anderen Gesamtstruktur ist, ist es jedoch keine Kerberos-Sitzungsschlüssel, mit dem zum Signieren und authentifizieren NTP-Pakete. Um die genaue uhrzeitsynchronisierung von einem Computer in einer anderen Gesamtstruktur abrufen, der Client benötigt Zugriff auf das Netzwerk auf diesem Computer und der Zeitdienst muss konfiguriert werden, um eine bestimmte Zeitquelle befindet sich in der anderen Gesamtstruktur verwenden. Wenn ein Client von einem NTP-Server außerhalb des eigenen Domänenhierarchie manuell Zugriffszeit konfiguriert ist, wird der NTP-Pakete zwischen dem Client und dem Zeitserver werden nicht authentifiziert, und sind daher nicht sicher. Auch bei der Implementierung von Gesamtstruktur-Vertrauensstellungen ist der Windows-Zeitdienst nicht in mehreren Gesamtstrukturen sicher. Obwohl der Anmeldedienst sichere Kanal der Authentifizierungsmethode für den Windows-Zeitdienst ist, wird die gesamtstrukturübergreifende Authentifizierung nicht unterstützt.  
  
#### <a name="hardware-devices-that-are-supported-by-the-windows-time-service"></a>Hardwaregeräte, die von der Windows-Zeitdienst unterstützt werden  
Hardware-basierten Uhren, z. B. GPS oder Radio Uhren werden häufig als präziser Verweis Uhr Geräte verwendet. Standardmäßig der Windows-Zeitdienst NTP-Zeitdienstanbieter unterstützt keine direkte Verbindung mit einem Hardwaregerät auf einem Computer, obwohl es möglich ist, erstellen Sie ein Software-basierte unabhängige Zeitanbieter unterstützt, die dieser Art der Verbindung. Diese Art von Anbieter, in Verbindung mit der Windows-Zeitdienst kann es sich um einen zuverlässigen und stabilen Zeit Verweis bereitstellen.  
  
Hardware-Geräte, z. B. eine Uhr Cesium oder einen Empfänger Global Positioning System (GPS) bieten genaue aktuelle Uhrzeit anhand der folgenden Standard um eine genaue Definition der Zeit zu erhalten. Cesium Uhren sind sehr stabile und sind nicht betroffen, durch Faktoren wie z. B. Temperatur, Druck oder Feuchtigkeit, aber es werden auch sehr kostspielig sein. Ein GPS-Empfänger ist sehr viel weniger teuer zu betrieben und auch eine genaue Verweis Uhr. GPS-Empfänger erhalten ihre Uhrzeit vom Satelliten, die Zeit von einer Uhr Cesium zu erhalten. Ohne eine unabhängige Zeitanbieter verwendet werden können Windows-Zeitserver Zeit erhalten, indem Sie Herstellen einer Verbindung mit einem externen NTP-Server, die mit einem Hardwaregerät über ein Telefon oder über das Internet verbunden ist. Organisationen, z. B. die U.s. Naval Observatory bieten NTP-Server, die mit äußerst zuverlässig Verweis Uhren verbunden sind.  
  
Viele GPS-Empfänger und anderen Geräten Zeit können als NTP-Server in einem Netzwerk fungieren. Sie können die AD DS-Gesamtstruktur, um Zeit von diesen Geräten externen Hardwarekomponenten zu synchronisieren, nur dann, wenn sie auch als NTP-Server in Ihrem Netzwerk fungieren konfigurieren. Konfigurieren Sie zu diesem Zweck des Domänencontrollers funktioniert als dem primären Domänencontroller (PDC)-Emulator im Stammverzeichnis Gesamtstruktur mit dem NTP-Server zur Verfügung gestellt, das GPS-Gerät synchronisieren. Zu diesem Zweck finden Sie unter [konfigurieren den Windows-Zeitdienst auf dem PDC-Emulator in der Gesamtstruktur-Stammdomäne](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29).  
  
### <a name="simple-network-time-protocol"></a>Simple Network Time Protocol  
SNTP Simple Network Time Protocol () ist eine vereinfachte Zeit-Protokoll, das für Server und Clients, die nicht mit der Genauigkeit benötigen, die NTP bereitstellt. SNTP, eine weitere einfache Version des NTP, ist das primäre Zeit-Protokoll, das in Windows 2000 verwendet wird. Da die Netzwerk-Paket-Formate von SNTP und NTP identisch sind, sind die zwei Protokolle interoperablen. Der Hauptunterschied zwischen den beiden ist, dass SNTP keinen Fehler Verwaltung und komplexe Filterung Systeme, die NTP enthält. Weitere Informationen über das Simple Network Time Protocol finden Sie unter RFC 1769 in der IETF RFC-Datenbank.  
  
### <a name="time-protocol-interoperability"></a>Zeit Protokoll Interoperabilität  
Windows-Zeitdienst kann in einer gemischten Umgebung von Computern unter Windows 2000, Windows XP und Windows Server 2003 verwendet werden, da das in Windows 2000 verwendete SNTP-Protokoll mit dem NTP-Protokoll in Windows XP und Windows Server 2003 kompatibel ist.  
  
Der Zeitdienst in Windows NT Server 4.0 aufgerufen TimeServ, synchronisiert die Uhrzeit in einer Windows NT 4.0-Netzwerk. TimeServ ist ein Add-on-Feature, das als Teil der *Microsoft Windows NT 4.0 Resource Kit* und verwendet nicht das Maß an Zuverlässigkeit der Synchronisierung, die von Windows Server 2003 erforderlich ist.  
  
Windows-Zeitdienst kann für die Interoperabilität mit Computern unter Windows NT 4.0, da die Zeit mit Windows 2000 oder Windows Server 2003-Computern synchronisiert werden können; ein Computer unter Windows 2000 oder Windows Server 2003 jedoch nicht automatisch auf Windows NT 4.0-Zeitserver ermitteln. Beispielsweise wenn Ihre Domäne konfiguriert ist, um Zeit zu synchronisieren, mit der Domäne, die Hierarchie basierende-Methode der Synchronisierung und Sie möchten Computer in der Domänenhierarchie Zeit mit einer Windows NT 4.0-Domänencontroller zu synchronisieren, stehen Ihnen so konfigurieren Sie diese Computer manuell zum Synchronisieren mit Windows NT 4.0-Domänencontroller.  
  
Windows NT 4.0 verwendet einen einfacheren Mechanismus für die zeitsynchronisierung als der Windows-Zeitdienst-Dienst verwendet. Aus diesem Grund wird um genau die zeitsynchronisierung in Ihrem Netzwerk zu gewährleisten, empfohlen, dass Sie alle Windows NT 4.0-Domänencontroller auf Windows 2000 oder Windows Server 2003 aktualisieren.  
  
## <a name="w2k3tr_times_how_izcr"></a>Windows Time Serviceprozesse und-Interaktionen  

Windows-Zeitdienst wurde entwickelt, um die Uhren von Computern in einem Netzwerk zu synchronisieren. Der Netzwerk Zeit, Zeit Konvergenz, die Abkürzung Synchronisierung in einem Netzwerk als jedem Zugriff auf Computer in einen genaueren-Server. Zeit Konvergenz umfasst einen Prozess, mit dem ein autorisierender Server die aktuelle Uhrzeit auf Clientcomputern in Form von NTP-Pakete enthält. Die Informationen in einem Paket angibt, ob eine Anpassung aktuelle Systemzeit des Computers gemacht werden, damit sie mit dem genauer Server synchronisiert werden muss.  
  
Im Rahmen der Zeit Konvergenz versuchen Mitglieder der Domäne, Zeit mit einem Domänencontroller in derselben Domäne befindet sich zu synchronisieren. Wenn der Computer ein Domänencontroller ist, wird versucht, die mit einem mehr autorisierenden Domänencontroller zu synchronisieren.  
  
Computer unter Windows XP Home Edition oder Computer, die nicht Mitglied einer Domäne sind versuchen Sie nicht mit der Domänenhierarchie synchronisieren, aber es sind standardmäßig so konfiguriert, von time.windows.com abzurufen.  
  
Um einen Computer unter Windows Server 2003 als autorisierend einzurichten, muss der Computer für die eine zuverlässige Zeitquelle konfiguriert werden. Standardmäßig ist der erste Domänencontroller, der in einer Windows Server 2003-Domäne installiert ist automatisch für eine zuverlässige Zeitquelle konfiguriert. Da es auf dem autorisierenden Computer für die Domäne ist, muss es konfiguriert werden und mit der Domänenhierarchie, nicht mit einer externen Zeitquelle synchronisieren. Außerdem werden standardmäßig alle anderen Windows Server 2003-Domänenmitglieder mit der Domänenhierarchie Synchronisierung konfiguriert.  
  
Wenn Sie ein Windows Server 2003-Netzwerk eingerichtet haben, können Sie die Windows-Zeitdienst um eine der folgenden Optionen für die Synchronisierung verwenden konfigurieren:  
  
-   Domäne Hierarchie-basierte Synchronisierung  
  
-   Eine manuell konfigurierte Synchronisierungsquelle  
  
-   Alle verfügbaren Verfahren  
  
-   Keine Synchronisierung.  
  
Jeder dieser Synchronisierungstypen wird im folgenden Abschnitt erläutert.  
  
### <a name="domain-hierarchy-based-synchronization"></a>Domäne Hierarchie-basierte Synchronisierung  

Synchronisierung, die basierend auf einer Domänenhierarchie verwendet die AD DS-Domäne-Hierarchie, um eine zuverlässige Quelle für die Synchronisierung von Zeit zu finden. Auf der Grundlage der Domänenhierarchie bestimmt der Windows-Zeitdienst die Genauigkeit der einzelnen Zeitserver. In einer Gesamtstruktur mit Windows Server 2003 enthält die Computer, der den primären Domänencontroller (PDC)-Emulator, befindet sich in der Stammdomäne der Gesamtstruktur Betriebsmasterfunktion die Position der besten Zeitquelle, es sei denn, eine andere zuverlässige Zeitquelle konfiguriert wurde. Die folgende Abbildung zeigt einen Pfad für die zeitsynchronisierung zwischen Computern in einer Domänenhierarchie.  
  
**Zeitsynchronisierung in einer AD DS-Hierarchie**  
  
![Windows-Zeitdienst](media/How-the-Windows-Time-Service-Works/trnt_ntw_adhc.gif)  
  
#### <a name="reliable-time-source-configuration"></a>Konfigurieren einer zuverlässigen Zeitquelle  
Ein Computer, der zuverlässige Zeitquelle konfiguriert ist, wird als Stamm der Zeitdienst identifiziert. Der Stamm des Zeitdiensts ist der autorisierende Server für die Domäne und in der Regel ist so konfiguriert, dass Zeit von einem externen NTP-Server oder das Gerät abrufen. Als zuverlässige Zeitquelle zu optimieren, wie in der gesamten Domänenhierarchie übertragen wird, kann ein Server konfiguriert werden. Wenn ein Domänencontroller eine zuverlässige Zeitquelle konfiguriert ist, kündigt Anmeldedienst diesen Domänencontroller als zuverlässige Zeitquelle, bei der Anmeldung mit dem Netzwerk. Wenn eine Zeitquelle für die Synchronisierung mit anderen Domänencontrollern suchen, wählen sie eine zuverlässige Quelle zuerst sofern verfügbar.  
  
#### <a name="time-source-selection"></a>Die ausgewählte Uhrzeit  
Der Prozess Zeit Quelle kann zwei Probleme in einem Netzwerk erstellen:  
  
-   Weitere Synchronisierung wechselt.  
  
-   Eine höhere Volumen des Netzwerkverkehrs.  
  
Ein Zyklus im Netzwerk Synchronisierung tritt auf, wenn die Zeit zwischen einer Gruppe von Domänencontrollern konsistent bleibt und gleichzeitig freigegeben ist, ohne eine erneute Synchronisierung mit einem anderen zuverlässige Zeitquelle fortlaufend. Der Windows-Zeitdienst Zeit Quelle Auswahl Algorithmus dient zum Schutz vor dieser Art von Problemen.  
  
Ein Computer verwendet eine der folgenden Methoden zum Synchronisieren mit eine Zeitquelle zu identifizieren:  
  
-   Wenn der Computer nicht Mitglied einer Domäne ist, muss es konfiguriert werden, um mit einer bestimmten Zeitquelle synchronisieren.  
  
-   Wenn der Computer auf einem Mitgliedsserver oder einer Arbeitsstation innerhalb einer Domäne, in der Standardeinstellung ist folgt die AD DS-Hierarchie und synchronisiert die Uhrzeit mit einem Domänencontroller in der lokalen Domäne, die Windows-Zeitdienst derzeit ausgeführt wird.  
  
Wenn der Computer ein Domänencontroller ist, ist es bis zu sechs Abfragen zum Synchronisieren mit einem anderen Domänencontroller zu suchen. Diese Abfrage dient zum Identifizieren einer Zeitquelle mit bestimmten Attributen, z. B. ein Domänencontroller an einem bestimmten Ort und davon, ob es sich um eine zuverlässige Zeitquelle ist. Die Zeitquelle muss auch die folgenden Einschränkungen beachtet werden:  
  
-   Zuverlässige Zeitquelle kann nur mit einem Domänencontroller in der übergeordneten Domäne synchronisieren.  
  
-   PDC-Emulator kann mit zuverlässige Zeitquelle in seiner eigenen Domäne oder einen beliebigen Domänencontroller in der übergeordneten Domäne synchronisieren.  
  
Ist der Domänencontroller nicht mit dem Domänencontroller synchronisiert, die es abfragt, wird die Abfrage nicht vorgenommen. Der Domänencontroller weiß, welche Art von Computer, die es Zeit von abrufen kann, bevor er die Abfrage wird. Z. B. versucht ein lokale PDC-Emulator auf Abfrage Zahlen drei oder sechs nicht, da ein Domänencontroller nicht versucht, die Synchronisierung mit sich selbst.  
  
Die folgende Tabelle enthält die Abfragen, die von einem Domänencontroller wird eine Zeitquelle und die Reihenfolge, in der die Abfragen vorgenommen werden.  
  
**Domain Controller-Zeitquelle Abfragen**  
  
|Anzahl der Abfrage|Domänencontroller|Speicherort|Zuverlässigkeit der Zeitquelle|  
|----------------|---------------------|------------|------------------------------|  
|1|Übergeordneten Domänencontroller|Am Standort|Bevorzugt eine zuverlässige Zeitquelle jedoch mit ohne zuverlässige Zeitquelle synchronisieren können, ist, die alle, die verfügbar ist.|  
|2|Lokale Domänencontroller|Am Standort|Nur synchronisiert mit einer zuverlässigen Zeitquelle.|  
|3|Lokale PDC-emulator|Am Standort|Wird nicht angewendet.<br /><br />Ein Domänencontroller versucht nicht, die Synchronisierung mit sich selbst.|  
|4|Übergeordneten Domänencontroller|Außerhalb des Standorts|Bevorzugt eine zuverlässige Zeitquelle jedoch mit ohne zuverlässige Zeitquelle synchronisieren können, ist, die alle, die verfügbar ist.|  
|5|Lokale Domänencontroller|Außerhalb des Standorts|Nur synchronisiert mit einer zuverlässigen Zeitquelle.|  
|6|Lokale PDC-emulator|Außerhalb des Standorts|Wird nicht angewendet.<br /><br />Ein Domänencontroller versucht nicht, die Synchronisierung mit sich selbst.|  
  
**Hinweis:**  
  
-   Ein Computer wird mit sich selbst nie synchronisiert. Wenn der Computer versucht, die Synchronisierung der lokalen PDC-Emulator ist, versucht er nicht Abfragen 3 oder 6.  
  
Diese Abfrage gibt eine Liste der Domänencontroller, die als Zeitquelle verwendet werden können. Windows-Zeitdienst weist jeder Domänencontroller abgefragt eine Bewertung basierend auf die Zuverlässigkeit und die Position des Domänencontrollers. Die folgende Tabelle enthält die Ergebnisse von Windows-Zeitdienst für jeden Domänencontroller zugewiesen.  
  
**Bewertung-Ermittlung**  
  
|Domänencontrollerstatus|Bewertung|  
|----------------------------|---------|  
|Domänencontroller, die sich in demselben Standort befindet|8|  
|Zuverlässige Zeitquelle als Domänencontroller|4|  
|Domänencontroller in der übergeordneten Domäne|2|  
|Domänencontroller, der PDC-Emulator ist|1|  
  
Wenn der Windows-Zeitdienst feststellt, dass sie den Domänencontroller mit dem besten mögliche Wert identifiziert hat, werden keine weitere Abfragen vorgenommen. Die Faktoren, die durch den Zeitdienst zugewiesen sind kumulativ, d. h., ein PDC-Emulator am gleichen Standort eine Bewertung von neun empfängt.  
  
Wenn im Stammverzeichnis der Zeitdienst nicht konfiguriert ist, um mit einer externen Quelle synchronisieren, steuert die interne Hardware Uhr des Computers die Zeit an.  
  
### <a name="manually-specified-synchronization"></a>Manuell konfigurierte Synchronisierung  
Manuell konfigurierte Synchronisierung können Sie einen einzelnen Peer oder eine Liste von Peers, von denen ein Computer Zeit erhält, festzulegen. Wenn der Computer nicht Mitglied einer Domäne ist, müssen sie manuell konfiguriert werden, um mit einer bestimmten Zeitquelle synchronisieren. Ein Computer, die ist, dass ein Mitglied einer Domäne in der Standardeinstellung für die Synchronisierung von der Domänenhierarchie konfiguriert ist, ist die manuell konfigurierte Synchronisierung besonders nützlich für den Stamm der Gesamtstruktur der Domäne oder für Computer, die nicht Mitglied einer Domäne sind. Manuelle Eingabe von einem externen NTP-Server zum Synchronisieren mit dem autorisierenden Computer für Ihre Domäne bietet eine zuverlässige Zeit. Konfigurieren des autorisierenden Computers für Ihre Domäne für die Synchronisierung mit einer Hardware-Uhr ist jedoch eine bessere Lösung für die Bereitstellung der genauesten und sicheren Zeit mit Ihrer Domäne.  
  
Manuell konfigurierte Zeitquellen werden nicht authentifiziert, es sei denn, ein spezieller Zeitanbieter für sie geschrieben wurde, und daher anfällig für Angriffe ist. Auch wenn ein Computer mit einer Quelle manuell angegeben, anstatt den authentifizierenden Domänencontroller synchronisiert wird, die beiden Computer nicht mehr synchron, verursacht der Kerberos-Authentifizierung fehlschlägt möglicherweise. Dies könnte andere Aktionen, die die Authentifizierung fehlschlägt, z. B. drucken oder Dateifreigabe erfordern. Wenn nur Stamm der Gesamtstruktur für die Synchronisierung mit einer externen Quelle konfiguriert ist, bleiben alle anderen Computer in der Gesamtstruktur synchronisiert, erschwert Replay-Angriffe.  
  
### <a name="all-available-synchronization-mechanisms"></a>Alle verfügbaren Verfahren  

Die Option "alle verfügbaren Verfahren" ist die wertvollsten Synchronisierungsmethode für Benutzer in einem Netzwerk. Diese Methode ermöglicht die Synchronisierung mit der Domänenhierarchie und bieten auch eine alternative Zeitquelle sollte die Domänenhierarchie, je nach Konfiguration verfügbar. Wenn der Client kann nicht mit der Domänenhierarchie Uhrzeit synchronisiert ist, die Zeitquelle automatisch fragt die Zeitquelle angegeben werden, indem Sie die **NtpServer** Einstellung. Diese Methode der Synchronisierung ist wahrscheinlich um genaue Uhrzeit für Clients bereitzustellen.  

### <a name="stopping-time-synchronization"></a>Synchronisierung beendet.  
Es gibt Situationen, in denen Sie eine Synchronisierung der Uhrzeit des Computers beenden möchten. Z. B. wenn ein Computer versucht, eine Zeitquelle im Internet oder von einem anderen Standort über ein WAN über eine DFÜ-Verbindung zu synchronisieren, können sie kostspielige Telefon anfallen. Wenn Sie die Synchronisierung auf diesem Computer deaktivieren, verhindern Sie das Zugriffsversuch auf eine Zeitquelle über eine DFÜ-Verbindung des Computers.  
  
Sie können auch die Synchronisierung, um zu verhindern, dass die Generierung von Fehlern im Ereignisprotokoll deaktivieren. Jedes Mal, wenn ein Computer versucht, mit einer Zeitquelle synchronisieren, die nicht verfügbar ist, wird einen Fehler im Ereignisprotokoll generiert. Wenn eine Zeitquelle aus dem Netzwerk für die geplante Wartung stammt und Sie nicht den Client für die Synchronisierung von einer anderen Quelle neu konfigurieren möchten, können Sie deaktivieren, Synchronisierung auf dem Client, um zu verhindern, dass Sie versuchen, Synchronisierung, während der Zeitserver nicht verfügbar ist.  
  
Es ist sinnvoll, deaktivieren Sie die Synchronisierung auf dem Computer, das als Stamm des Netzwerks Synchronisierung festgelegt ist. Dies weist darauf hin, dass der Computer Stamm ihrer lokale Uhr vertraut. Wenn im Stammverzeichnis der Hierarchie Synchronisierung nicht, um festgelegt ist **NoSync** und ist er nicht mit einem anderen Zeitquelle synchronisieren, Clients akzeptieren keine das Paket, das diesen Computer versendet, da seine Zeit nicht vertrauenswürdig ist.  
  
Nur dann sind Server, die von den Clients als vertrauenswürdig eingestuft werden, auch wenn sie nicht mit einem anderen Zeitquelle synchronisiert haben, die vom Client als zuverlässigen Zeitserver identifiziert wurden.  
  
### <a name="disabling-the-windows-time-service"></a>Deaktivieren des Windows-Zeitdienstes  
Windows-Zeitdienst (W32Time) kann vollständig deaktiviert werden. Bei Auswahl ein Produkts zur Synchronisierung von Drittanbietern Zeit zu implementieren, das NTP-Server verwendet wird, müssen Sie die Windows-Zeitdienst deaktivieren. Dies ist, da alle NTP-Server Zugriff auf UDP-Port 123 (UDP = User Datagram Protocol benötigen), und wie die Windows-Zeitdienst auf dem Betriebssystem Windows Server 2003 ausgeführt wird, Port 123 durch Windows-Zeitdienst reserviert bleibt.  
  
## <a name="w2k3tr_times_how_ydum"></a>Netzwerk-Ports, die von Windows-Zeitdienst verwendet  
Windows-Zeitdienst kommuniziert in einem Netzwerk ermitteln von zuverlässigen Quellen, erhalten Informationen zum Zeitpunkt des und Informationen mit anderen Computern bereitstellen. Diese Kommunikation wird ausgeführt, durch die NTP und SNTP-RFCs definiert.  
  
**Letztere erfolgt für den Windows-Zeitdienst**  
  
|Dienstname|UDP|TCP|  
|----------------|-------|-------|  
|NTP|123|N/V|  
|SNTP|123|N/V|  
  
## <a name="see-also"></a>Siehe auch  
[Technische Referenz zu Windows Time Service](https://technet.microsoft.com/library/cc773061.aspx)  
[Windows-Zeitdienst: Tools und Einstellungen](Windows-Time-Service-Tools-and-Settings.md)  
[Microsoft Knowledge Base-Artikel 902229](https://go.microsoft.com/fwlink/?LinkId=186066)  
  


