---
title: route_ws2008
description: Erfahren Sie, wie Einträge in der lokalen IP-Routing Tabelle geändert und angezeigt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: afcd666c-0cef-47c2-9bcc-02d202b983b3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: a0287fed8452cb155ea858ff0a544962dd765c3a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835603"
---
# <a name="route_ws2008"></a>route_ws2008

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt die Einträge in der lokalen IP-Routing Tabelle an und ändert Sie. Wird ohne Parameter verwendet, die **Route** zeigt Hilfe an.   

## <a name="syntax"></a>Syntax  
```  
route [/f] [/p] [<Command> [<Destination>] [mask <Netmask>] [<Gateway>] [metric <Metric>]] [if <Interface>]]  
```  

#### <a name="parameters"></a>Parameter  

|Parameter|Beschreibung|  
|-------|--------|  
|/f|Löscht die Routing Tabelle aller Einträge, die keine Host Routen sind (Routen mit einer Netzmaske von 255.255.255.255), der Loopback-Netzwerk Route (Routen mit dem Ziel 127.0.0.0 und einer Netzmaske von 255.0.0.0) oder einer Multicast Route (Routen mit dem Ziel 224.0.0.0 und einer Netzmaske von 240.0.0.0). Wenn dies in Verbindung mit einem der Befehle (z. b. "hinzufügen", "ändern" oder "Löschen") verwendet wird, wird die Tabelle vor dem Ausführen des Befehls gelöscht.|  
|/p|Bei Verwendung mit dem Add-Befehl wird die angegebene Route der Registrierung hinzugefügt und zum Initialisieren der IP-Routing Tabelle verwendet, wenn das TCP/IP-Protokoll gestartet wird. Standardmäßig werden hinzugefügte Routen nicht beibehalten, wenn das TCP/IP-Protokoll gestartet wird. Bei Verwendung mit dem Print-Befehl wird die Liste der persistenten Routen angezeigt. Dieser Parameter wird für alle anderen Befehle ignoriert. Persistente Routen werden am Registrierungs Speicherort **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\tcpip\parameters\persistentroutes**gespeichert.|  
|\<Befehl >|Gibt den Befehl an, den Sie ausführen möchten. In der folgenden Tabelle sind die gültigen Befehle aufgeführt:<p>-   **hinzufügen:** fügt eine Route hinzu.<br />-   **Änderung:** ändert eine vorhandene Route.<br />-   **delete:** löscht eine Route oder Routen.<br />-   **Print:** druckt eine Route oder Routen.|  
|\<Ziel >|Gibt das Netzwerk Ziel der Route an. Bei dem Ziel kann es sich um eine IP-Netzwerkadresse (bei der die Hostbits der Netzwerkadresse auf 0 festgelegt sind), eine IP-Adresse für eine Hostroute oder 0.0.0.0 für die Standardroute handeln.|  
|Maske \<Netzmaske >|Gibt das Netzwerk Ziel der Route an. Bei dem Ziel kann es sich um eine IP-Netzwerkadresse (bei der die Hostbits der Netzwerkadresse auf 0 festgelegt sind), eine IP-Adresse für eine Hostroute oder 0.0.0.0 für die Standardroute handeln.|  
|\<Gateway >|Gibt die IP-Adresse für den Weiterleitungs-oder nächsten Hop an, über die die vom Netzwerk Ziel und der Subnetzmaske definierten Adressen erreichbar sind. Bei lokal angehängten Subnetzrouten ist die Gatewayadresse die IP-Adresse, die der Schnittstelle zugewiesen ist, die mit dem Subnetz verbunden ist. Bei Remote Routen, die auf einem oder mehreren Routern verfügbar sind, ist die Gatewayadresse eine direkt erreichbare IP-Adresse, die einem benachbarten Router zugewiesen wird.|  
|Metrik \<Metrik >|Gibt eine ganzzahlige Kosten Metrik (von 1 bis 9999) für die Route an, die bei der Auswahl mehrerer Routen in der Routing Tabelle verwendet wird, die am ehesten mit der Zieladresse eines weitergeleiteten Pakets übereinstimmen. Die Route mit der niedrigsten Metrik wird ausgewählt. Die Metrik kann die Anzahl der Hops, die Geschwindigkeit des Pfades, die Pfad Zuverlässigkeit, den Pfad Durchsatz oder administrative Eigenschaften widerspiegeln.|  
|Wenn \<-Schnittstelle >|Gibt den Schnittstellen Index für die Schnittstelle an, über die das Ziel erreichbar ist. Eine Liste der Schnittstellen und der zugehörigen Schnittstellen Indizes finden Sie in der Anzeige des Befehls Route Print. Sie können für den Schnittstellen Index entweder Dezimal-oder hexadezimale Werte verwenden. Stellen Sie bei hexadezimalen Werten der hexadezimalen Zahl 0x voran. Wenn der if-Parameter weggelassen wird, wird die-Schnittstelle von der Gatewayadresse bestimmt.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
- Große Werte in der Spalte **Metrik** der Routing Tabelle sind das Ergebnis, dass TCP/IP die Metrik für Routen in der Routing Tabelle basierend auf der Konfiguration von IP-Adresse, Subnetzmaske und Standard Gateway für jede LAN-Schnittstelle automatisch ermitteln kann. Die automatische Bestimmung der Schnittstellen Metrik, die standardmäßig aktiviert ist, bestimmt die Geschwindigkeit der einzelnen Schnittstellen und passt die Metriken der Routen für jede Schnittstelle an, sodass mit der schnellsten Schnittstelle die Routen mit der niedrigsten Metrik erstellt werden. Deaktivieren Sie zum Entfernen der großen Metriken die automatische Ermittlung der Schnittstellen Metrik aus den erweiterten Eigenschaften des TCP/IP-Protokolls für jede LAN-Verbindung.  
- Namen können für das *Ziel* verwendet werden, wenn ein entsprechender Eintrag in der lokalen Netzwerkdatei vorhanden ist, die im Ordner <strong>systemroot\system32\drivers\\</strong>usw. gespeichert ist. Namen können für das *Gateway* verwendet werden, sofern Sie über standardmäßige Host namens Auflösungs Techniken wie Domain Name System (DNS)-Abfragen in eine IP-Adresse aufgelöst werden können, die im Ordner <strong>systemroot\system32\drivers\\</strong>usw. gespeicherte Datei local Hosts und die NetBIOS-Namensauflösung.  
- Wenn der Befehl **gedruckt** oder **gelöscht**wird, kann der Gatewayparameter ausgelassen werden, und Platzhalter können für das Ziel und das Gateway verwendet werden. *Gateway* Der *Zielwert* kann ein Platzhalter Wert sein, der durch ein Sternchen (*) angegeben wird. Wenn das angegebene Ziel ein Sternchen (\*) oder ein Fragezeichen (?) enthält, wird es als Platzhalter behandelt, und nur übereinstimmende Ziel Routen werden gedruckt oder gelöscht. Das Sternchen entspricht einer beliebigen Zeichenfolge, und das Fragezeichen entspricht einem beliebigen einzelnen Zeichen. Beispiel: 10.\*. 1, 192,168.\*, 127.\*und \*224\* sind alle gültigen Verwendungen des Sternchen-Platzhalters.  
- Wenn Sie eine ungültige Kombination eines Werts für Ziel und Subnetzmaske (netmask) verwenden, wird die Fehlermeldung "Route: Ungültige Gatewayadresse netmask" angezeigt. Diese Fehlermeldung wird angezeigt, wenn das Ziel ein oder mehrere Bits enthält, die in Bitpositionen auf 1 festgelegt sind, wenn das entsprechende Subnetzmaske-Bit auf 0 festgelegt ist. Um diese Bedingung zu testen, können Sie das Ziel und die Subnetzmaske mithilfe der Binär Notation Ausdrücken. Die Subnetzmaske in der binären Notation besteht aus einer Reihe von 1 Bits, die den Netzwerk Adress Teil des Ziels darstellen, und einer Reihe von 0 Bits, die den Host Adress Teil des Ziels darstellt. Überprüfen Sie, ob im Ziel Bits vorhanden sind, die für den Teil des Ziels, der die Host Adresse ist (wie durch die Subnetzmaske definiert), auf 1 festgelegt sind.  
- Der **/p** -Parameter wird nur auf dem Routen Befehl für Windows NT 4,0, Windows 2000, Windows Millennium Edition, Windows XP und Windows Server 2003 unterstützt. Dieser Parameter wird vom **Routen** Befehl für Windows 95 oder Windows 98 nicht unterstützt.  
- Dieser Befehl ist nur verfügbar, wenn das TCP/IP-Protokoll (Internet Protocol) als Komponente in den Eigenschaften eines Netzwerkadapters in Netzwerkverbindungen installiert ist.  

## <a name="examples"></a><a name="BKMK_Examples"></a>Beispiele  
Geben Sie Folgendes ein, um den gesamten Inhalt der IP-Routing Tabelle anzuzeigen:  
```  
route print  
```  
Um die Routen in der IP-Routing Tabelle anzuzeigen, die mit 10 beginnen, geben Sie Folgendes ein:  
```  
route print 10.*  
```  
Um eine Standardroute mit der Standardgatewayadresse von 192.168.12.1 hinzuzufügen, geben Sie Folgendes ein:  
```  
route add 0.0.0.0 mask 0.0.0.0 192.168.12.1  
```  
Um eine Route zum Ziel 10.41.0.0 mit der Subnetzmaske 255.255.0.0 und der Adresse des nächsten Hops von 10.27.0.1 hinzuzufügen, geben Sie Folgendes ein:  
```  
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1  
```  
Zum Hinzufügen einer permanenten Route zum Ziel 10.41.0.0 mit der Subnetzmaske 255.255.0.0 und der Adresse des nächsten Hops von 10.27.0.1 geben Sie Folgendes ein:  
```  
route /p add 10.41.0.0 mask 255.255.0.0 10.27.0.1  
```  
Geben Sie Folgendes ein, um eine Route zum Ziel 10.41.0.0 mit der Subnetzmaske 255.255.0.0, der Adresse 10.27.0.1 für den nächsten Hop und der Kosten Metrik 7 hinzuzufügen:  
```  
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1 metric 7  
```  
Um eine Route zum Ziel 10.41.0.0 mit der Subnetzmaske 255.255.0.0, der Adresse des nächsten Hops von 10.27.0.1 und dem Schnittstellen Index 0x3 hinzuzufügen, geben Sie Folgendes ein:  
```  
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1 if 0x3  
```  
Um die Route zum Ziel 10.41.0.0 mit der Subnetzmaske 255.255.0.0 zu löschen, geben Sie Folgendes ein:  
```  
route delete 10.41.0.0 mask 255.255.0.0  
```  
Um alle Routen in der IP-Routing Tabelle zu löschen, die mit 10 beginnen, geben Sie Folgendes ein:  
```  
route delete 10.*  
```  
Um die Adresse des nächsten Hops der Route mit dem Ziel 10.41.0.0 und der Subnetzmaske von 255.255.0.0 von 10.27.0.1 in 10.27.0.25 zu ändern, geben Sie Folgendes ein:  
```  
route change 10.41.0.0 mask 255.255.0.0 10.27.0.25  
```  

## <a name="additional-references"></a>Weitere Verweise  
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
