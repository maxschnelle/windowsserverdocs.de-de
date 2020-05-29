---
title: Verwenden der automatischen TCP/IP-Adressierung ohne DHCP-Server
description: Einführung in die Verwendung der automatischen TCP/IP-Adressierung ohne DHCP-Server.
ms.date: 5/26/2020
ms.prod: windows-server
ms.service: na
manager: dcscontentpm
ms.technology: server-general
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.reviewer: robsmi
ms.openlocfilehash: 8fbde77381141b76959f70e824eac22ee2121fa3
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2020
ms.locfileid: "84150188"
---
# <a name="how-to-use-automatic-tcpip-addressing-without-a-dhcp-server"></a>Verwenden der automatischen TCP/IP-Adressierung ohne DHCP-Server

In diesem Artikel wird beschrieben, wie Sie die automatische TCP/IP-Adressierung (Transmission Control Protocol/Internet Protocol) verwenden, ohne dass ein DHCP-Server (Dynamic Host Configuration-Protokoll) im Netzwerk vorhanden ist. Die im Abschnitt "betrifft" dieses Artikels aufgeführten Betriebssystemversionen verfügen über eine Funktion namens "automatische private IP-Adressierung" (APIPA). Mit diesem Feature kann ein Windows-Computer sich selbst eine IP-Adresse zuweisen, wenn ein DHCP-Server nicht verfügbar oder nicht im Netzwerk vorhanden ist. Diese Funktion macht das Konfigurieren und unterstützen eines kleinen LAN (Local Area Network), auf dem TCP/IP ausgeführt wird, weniger schwierig.

## <a name="more-information"></a>Weitere Informationen

> [!IMPORTANT]  
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/help/322756) für den Fall, dass Probleme auftreten.

Ein Windows-basierter Computer, der für die Verwendung von DHCP konfiguriert ist, kann sich automatisch eine IP-Adresse zuweisen, wenn kein DHCP-Server verfügbar ist. Dies kann beispielsweise in einem Netzwerk ohne DHCP-Server oder in einem Netzwerk vorkommen, wenn ein DHCP-Server vorübergehend zur Wartung ausfällt.

Die Internet Assigned Numbers Authority (IANA) hat 169.254.0.0-169.254.255.255 für die automatische private IP-Adressierung reserviert. Das Ergebnis ist, dass APIPA eine Adresse bereitstellt, die garantiert nicht mit Routing fähigen Adressen in Konflikt steht.

Nachdem dem Netzwerkadapter eine IP-Adresse zugewiesen wurde, kann der Computer TCP/IP für die Kommunikation mit einem beliebigen anderen Computer verwenden, der mit dem gleichen LAN verbunden ist und auch für APIPA konfiguriert ist oder die IP-Adresse manuell auf 169.254. x. y festgelegt ist (wobei x. y der eindeutige Bezeichner des Clients ist) und die Subnetzmaske 255.255.0.0 aufweist. Beachten Sie, dass der Computer nicht mit Computern in anderen Subnetzen oder mit Computern kommunizieren kann, die keine automatische private IP-Adressierung verwenden. Die automatische private IP-Adressierung ist standardmäßig aktiviert.

Möglicherweise möchten Sie die Datei in einem der folgenden Fälle deaktivieren:

- Ihr Netzwerk verwendet Router.

- Ihr Netzwerk ist ohne NAT-oder Proxy Server mit dem Internet verbunden.

Wenn Sie keine DHCP-bezogenen Meldungen deaktiviert haben, erhalten Sie mithilfe von DHCP-Nachrichten eine Benachrichtigung, wenn Sie zwischen DHCP-Adressierung und automatischer privater IP-Adressierung wechseln Wenn das DHCP-Messaging versehentlich deaktiviert wird, können Sie die DHCP-Nachrichten wieder aktivieren, indem Sie den Wert des Werts "PopupFlag" im folgenden Registrierungsschlüssel von 00 auf 01 ändern:  
`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\DHCP` 

Beachten Sie, dass Sie den Computer neu starten müssen, damit die Änderung wirksam wird. Sie können auch bestimmen, ob der Computer APIPA verwendet, indem Sie das Winipcfg-Tool in Windows Millennium Edition, Windows 98 oder Windows 98 Second Edition verwenden:

Klicken Sie auf Start, klicken Sie auf Ausführen, geben Sie "Winipcfg" (ohne Anführungszeichen) ein, und klicken Sie dann auf OK. Klicken Sie auf Weitere Informationen. Wenn das IP-Adressfeld für die automatische IP-Adresse eine IP-Adresse im Bereich 169.254. x. x enthält, wird die automatische private IP-Adressierung aktiviert. Wenn das Feld IP-Adresse vorhanden ist, ist die automatische private IP-Adressierung zurzeit nicht aktiviert.
Für Windows 2000, Windows XP oder Windows Server 2003 können Sie mithilfe des Befehls "ipconfig" an einer Eingabeaufforderung ermitteln, ob der Computer APIPA verwendet:

Klicken Sie im Startmenü auf Ausführen, geben Sie "cmd" (ohne Anführungszeichen) ein, und klicken Sie dann auf OK, um ein MS-DOS-Befehlszeilenfenster zu öffnen. Geben Sie "ipconfig/all" (ohne Anführungszeichen) ein, und drücken Sie dann die EINGABETASTE. Wenn die Zeile "automatische Konfiguration aktiviert" den Wert "yes" hat und "Autoconfiguration IP Address" den Wert "169.254. x. y" hat (wobei "x. y" der eindeutige Bezeichner des Clients ist), verwendet der Computer APIPA. Wenn die Zeile "automatische Konfiguration aktiviert" den Wert "No" (Nein) anzeigt, verwendet der Computer derzeit nicht APIPA.
Sie können die automatische private IP-Adressierung deaktivieren, indem Sie eine der folgenden Methoden verwenden.

Sie können die TCP/IP-Informationen manuell konfigurieren, wodurch DHCP vollständig deaktiviert wird. Sie können die automatische private IP-Adressierung (aber nicht DHCP) deaktivieren, indem Sie die Registrierung bearbeiten. Fügen Sie hierzu den DWORD-Registrierungs Eintrag "ipautoconfigurationaktivierte DWORD" mit dem Wert "0x0" zum folgenden Registrierungsschlüssel für Windows Millennium Edition, Windows98 oder Windows 98 Second Edition hinzu:`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\VxD\DHCP`

Für Windows 2000, Windows XP und Windows Server 2003 kann APIPA deaktiviert werden, indem der DWORD-Registrierungs Eintrag "ipautoconfigurationaktivierter DWORD" mit dem Wert "0x0" dem folgenden Registrierungsschlüssel hinzugefügt wird:  
`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\<Adapter GUID>`  
> [!NOTE]
> Der **GUID** -Unterschlüssel für den Adapter ist eine Globally Unique Identifier (GUID) für den LAN-Adapter des Computers.

Wenn Sie den Wert 1 für den ipauteconfigurationenable DWORD-Eintrag angeben, wird APIPA aktiviert, was der Standardstatus ist, wenn dieser Wert in der Registrierung ausgelassen wird.

## <a name="examples-of-where-apipa-may-be-useful"></a>Beispiele dafür, wo APIPA nützlich sein kann

### <a name="example-1-no-previous-ip-address-and-no-dhcp-server"></a>Beispiel 1: keine vorherige IP-Adresse und kein DHCP-Server

Wenn Ihr Windows-basierter Computer (für DHCP konfiguriert) initialisiert wird, werden drei oder mehr "Discover"-Nachrichten übermittelt. Wenn ein DHCP-Server nicht antwortet, nachdem mehrere Ermittlungs Meldungen gesendet wurden, weist der Windows-Computer sich selbst eine APIPA-Adresse (Class B) zu. Anschließend zeigt der Windows-Computer eine Fehlermeldung an den Benutzer des Computers an (es wird sichergestellt, dass ihm in der Vergangenheit nie eine IP-Adresse von einem DHCP-Server zugewiesen wurde). Der Windows-Computer sendet dann alle drei Minuten eine Ermittlungs Nachricht, um eine Kommunikation mit einem DHCP-Server herzustellen.

### <a name="example-2-previous-ip-address-and-no-dhcp-server"></a>Beispiel 2: vorherige IP-Adresse und kein DHCP-Server

Der Computer überprüft, ob der DHCP-Server vorhanden ist. wird er nicht gefunden, wird versucht, das Standard Gateway zu kontaktieren. Wenn das Standard Gateway antwortet, behält der Windows-Computer die zuvor geleast IP-Adresse bei. Wenn auf dem Computer jedoch keine Antwort vom Standard Gateway empfangen wird oder keine Antwort zugewiesen ist, verwendet er die automatische private IP-Adressierungs Funktion, um sich selbst eine IP-Adresse zuzuweisen. Dem Benutzer wird eine Fehlermeldung angezeigt, und die Nachrichten werden alle drei Minuten übermittelt. Sobald ein DHCP-Server Online ist, wird eine Meldung generiert, die besagt, dass die Kommunikation mit einem DHCP-Server wieder hergestellt wurde.

### <a name="example-3-lease-expires-and-no-dhcp-server"></a>Beispiel 3: Lease läuft ab und kein DHCP-Server

Der Windows-basierte Computer versucht, die Lease der IP-Adresse wiederherzustellen. Wenn auf dem Windows-Computer kein DCHP-Server gefunden wird, wird eine IP-Adresse zugewiesen, nachdem eine Fehlermeldung erzeugt wurde. Der Computer überträgt dann vier Discover-Nachrichten, und nach fünf Minuten wird das gesamte Verfahren wiederholt, bis ein DHCP-Server Online ist. Daraufhin wird eine Meldung generiert, die besagt, dass die Kommunikation mit dem DHCP-Server wieder hergestellt wurde.
