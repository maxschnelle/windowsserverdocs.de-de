---
title: route_ws2008
description: Informationen Sie zum Ändern und die Einträge in der lokalen IP-Routingtabelle angezeigt.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afcd666c-0cef-47c2-9bcc-02d202b983b3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 1164767a80b4d7dd24152bc34eda5d88834c1bdb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854821"
---
# <a name="routews2008"></a>route_ws2008

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt an, und ändert die Einträge in der lokalen IP-Routingtabelle. Ohne Parameter verwendet **Route** zeigt die Hilfe.   

## <a name="syntax"></a>Syntax  
```  
route [/f] [/p] [<Command> [<Destination>] [mask <Netmask>] [<Gateway>] [metric <Metric>]] [if <Interface>]]  
```  

### <a name="parameters"></a>Parameter  

|Parameter|Beschreibung|  
|-------|--------|  
|/f|Löscht die Routingtabelle aller Einträge, die nicht Hostrouten (Routen mit der Netzmaske 255.255.255.255), der Loopback-Netzwerkroute (Routen mit dem Ziel 127.0.0.0 und Netzmaske 255.0.0.0) oder eine multicast-Route (Routen mit dem Ziel 224.0.0.0 und der Netzmaske 240.0.0.0). Wenn Sie dies zusammen mit einem der Befehle (z. B. hinzufügen, ändern oder löschen) verwendet wird, wird die Tabelle gelöscht, vor dem Ausführen des Befehls.|  
|/p|Bei Verwendung mit dem Befehl hinzufügen, wird die angegebene Route wird in der Registrierung hinzugefügt und wird verwendet, um die IP-Routingtabelle zu initialisieren, wenn das TCP/IP-Protokoll gestartet wird. Hinzugefügte Routen werden standardmäßig nicht beibehalten, wenn das TCP/IP-Protokoll gestartet wird. Wenn mit dem Drucken-Befehl verwendet wird, wird die Liste der persistenten Routen angezeigt. Dieser Parameter wird für alle andere Befehle ignoriert. Persistente Routen werden Stelle in der Registrierung gespeichert **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\PersistentRoutes**.|  
|\<Befehl >|Gibt den Befehl aus, die, den Sie ausführen möchten. Die folgende Tabelle enthält die gültigen Befehle:<br /><br />-   **Fügen Sie hinzu:** Fügt eine Route hinzu.<br />-   **ändern:** ändert eine vorhandene Route.<br />-   **Löschen:** Löscht eine oder mehrere Routen.<br />-   **Drucken:** gibt eine oder mehrere Routen.|  
|\<Ziel >|Gibt an, das Netzwerkziel der Route. Das Ziel kann sein, eine IP-Netzwerkadresse, die (in der Netzwerkadresse die Hostbits auf 0 festgelegt sind), eine IP-Adresse für eine Hostroute oder "0.0.0.0" für die Standardroute.|  
|Maske \<Netzmaske >|Gibt an, das Netzwerkziel der Route. Das Ziel kann sein, eine IP-Netzwerkadresse, die (in der Netzwerkadresse die Hostbits auf 0 festgelegt sind), eine IP-Adresse für eine Hostroute oder "0.0.0.0" für die Standardroute.|  
|\<Gateway>|Gibt an, die Weiterleitung oder der nächste Hop IP-Adresse für die der Satz von Adressen, die durch die Netzwerk-Ziel und die Subnetzmaske definiert erreichbar sind. Für lokal verbundenen Subnetzrouten ist die Gatewayadresse die IP-Adresse der Schnittstelle, die mit dem Subnetz verbunden ist. Für remote-Routen ist verfügbar auf einem oder mehreren Routern, die Gateway-Adresse eine direkte erreichbare IP-Adresse, die benachbarten Routers zugewiesen ist.|  
|Metrik \<Metrik >|Gibt eine ganze Zahl Kostenmetrik (zwischen 1 und 9999) für die Route, die verwendet wird, wenn mehrere Routen in der Routingtabelle auswählen, die die Zieladresse der weitergeleiteten Pakets am ehesten entsprechen. Es wird die Route mit der niedrigsten Metrik ausgewählt. Die Metrik kann widerspiegeln, die Anzahl der Hops, die den Pfad, Zuverlässigkeit, Pfaddurchsatz oder die administrative Eigenschaften.|  
|Wenn \<Schnittstelle >|Gibt an, den Schnittstellenindex der Schnittstelle, die über die das Ziel erreichbar ist. Verwenden Sie eine Liste von Schnittstellen und die zugehörigen Schnittstellenindizes die dem Befehl Route print. Sie können entweder Dezimal oder hexadezimal-Werte für den Index verwenden. Bei Hexadezimalwerten die hexadezimale Zahl mit 0 X vorangestellt werden. Wenn der Parameter fehlt, wird die Schnittstelle von der Gatewayadresse bestimmt.|  
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|  

## <a name="remarks"></a>Hinweise  
-   Große Werte in der **Metrik** Spalte der Routingtabelle werden daher, dass der TCP/IP aus, um die Metrik für Routen in der Routingtabelle, die auf Basis der Konfiguration der IP-Adresse, Subnetzmaske und Standardgateway automatisch zu ermitteln für jede LAN-Schnittstelle. Automatische Ermittlung der Schnittstellenmetrik, standardmäßig aktiviert, bestimmt der Geschwindigkeit der einzelnen Schnittstellen und passt die Metrik der Routen für jede Schnittstelle, sodass die schnellste Schnittstelle die Routen mit der niedrigsten Metrik erstellt. Um die große Metriken zu entfernen, deaktivieren Sie die automatische Ermittlung der Schnittstellenmetrik in der erweiterten Eigenschaften des TCP/IP-Protokolls für jede LAN-Verbindung.  
-   Namen können verwendet werden, für die *Ziel* Wenn ein entsprechenden Eintrag in der lokalen Netzwerke-Datei, die in gespeicherten vorhanden ist. die **systemroot\System32\Drivers\\**usw. Ordner. Namen können verwendet werden, für die *Gateway* so lange sie in eine IP-Adresse über standard hostnamensauflösung wie z. B. Abfragen von Domain Name System (DNS) aufgelöst werden können, verwenden die lokale Hosts-Datei gespeichert, der  **systemroot\system32\drivers\\**usw.-Ordner und NetBIOS-namensauflösung.  
-   Wenn der Befehl ist **Drucken** oder **löschen**, *Gateway* Parameter kann ausgelassen werden, und Platzhalter können für das Ziel und das Gateway verwendet werden. Die *Ziel* Wert kann einen Platzhalterwert, der durch ein Sternchen (*) angegeben sein. Wenn das angegebene Ziel ein Sternchen enthält (\*) oder ein Fragezeichen (?), wird er als Platzhalterzeichen behandelt und nur übereinstimmenden Zielrouten gedruckt oder gelöscht werden. Das Sternchen entspricht einer beliebigen Zeichenfolge aus, und das Fragezeichen entspricht einem beliebigen einzelnes Zeichen. Z. B. 10. \*.1 "," 192.168. \*, 127. \*, und \*224\* alle gültigen verwendet den Sternchen-Platzhalter.  
-   Zeigt eine ungültige Kombination aus einen Zielwert und Subnetz Netzwerkmaske ein "Route: Ungültige Gatewayadresse Netmask" Fehlermeldung angezeigt. Diese Fehlermeldung wird angezeigt, wenn das Ziel enthält ein oder mehrere Bits im Bit-Speicherorte, in dem entsprechenden Subnetz Mask Bits auf 0 festgelegt ist, auf 1 festgelegt. Um diese Bedingung zu testen, drücken Sie die Ziel und die Subnetzmaske Binärschreibweise verwenden. Die Subnetzmaske in binärer Notation besteht aus einer Reihe von 1 Bit, das darstellt, der Netzwerk-Adressteil des Ziels und eine Reihe von 0 Bits, die den Hostteil der Adresse des Ziels darstellt. Bestimmen Sie, ob Bits im Ziel, die für den Teil des Ziels auf 1, die die Adresse des Hosts festgelegt werden (wie durch die Subnetzmaske definiert) überprüfen.  
-   Die **/p** Parameter wird nur der Befehl Route für Windows NT 4.0, Windows 2000, Windows Millennium Edition, Windows XP und Windows Server 2003 unterstützt. Dieser Parameter wird nicht von der **Route** Befehl für Windows 95 oder Windows 98.  
-   Dieser Befehl ist nur verfügbar, wenn das Internetprotokoll (TCP/IP)-Protokoll als Komponente in den Eigenschaften eines Netzwerkadapters in den Netzwerkverbindungen installiert ist.  

## <a name="BKMK_Examples"></a>Beispiele für  
Um den gesamten Inhalt der IP-Routingtabelle anzuzeigen, geben Sie Folgendes ein:  
```  
route print  
```  
Zum Anzeigen von Routen in der IP-Routingtabelle, die mit 10 beginnen, geben Sie Folgendes ein:  
```  
route print 10.*  
```  
Um eine Standardroute mit die Adresse des Standardgateways 192.168.12.1 hinzuzufügen, geben Sie Folgendes ein:  
```  
route add 0.0.0.0 mask 0.0.0.0 192.168.12.1  
```  
Um eine Route zum Ziel 10.41.0.0 mit der Subnetzmaske 255.255.0.0 zuweisen und die Adresse des nächsten Hops 10.27.0.1 hinzuzufügen, geben Sie Folgendes ein:  
```  
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1  
```  
Um eine persistente Route zum Ziel 10.41.0.0 mit der Subnetzmaske 255.255.0.0 zuweisen und die Adresse des nächsten Hops 10.27.0.1 hinzuzufügen, geben Sie Folgendes ein:  
```  
route /p add 10.41.0.0 mask 255.255.0.0 10.27.0.1  
```  
Zum Hinzufügen einer Route zum Ziel 10.41.0.0 mit der Subnetzmaske 255.255.0.0 zuweisen, die Adresse des nächsten Hops 10.27.0.1 und die Kostenmetrik 7, geben Sie Folgendes ein:  
```  
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1 metric 7  
```  
Die Adresse des nächste Hops 10.27.0.1 und verwenden den Index 0 x 3, geben Sie zum Hinzufügen einer Route zum Ziel 10.41.0.0 mit der Subnetzmaske 255.255.0.0 zuweisen:  
```  
route add 10.41.0.0 mask 255.255.0.0 10.27.0.1 if 0x3  
```  
Um die Route zum Ziel 10.41.0.0 mit der Subnetzmaske 255.255.0.0 zu löschen, geben Sie Folgendes ein:  
```  
route delete 10.41.0.0 mask 255.255.0.0  
```  
Um alle Routen in der IP-Routingtabelle, die beginnen mit 10 zu löschen, geben Sie Folgendes ein:  
```  
route delete 10.*  
```  
Um der nächsten Hopadresse der Route mit dem Ziel 10.41.0.0 und der Subnetzmaske 255.255.0.0 aus 10.27.0.1 in 10.27.0.25 ändern möchten, geben Sie Folgendes ein:  
```  
route change 10.41.0.0 mask 255.255.0.0 10.27.0.25  
```  

## <a name="additional-references"></a>Zusätzliche Referenzen  
-   [Befehlszeilensyntax](command-line-syntax-key.md)  
