---
title: Problembehandlung bei SMB Multichannel
description: Führt SMB Multichannel-Methoden zur Problembehandlung ein.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 662a58fdeb3cda14a0e54c8d0ab7bd0b85387fd7
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86960132"
---
# <a name="smb-multichannel-troubleshooting"></a>Problembehandlung bei SMB Multichannel

In diesem Artikel wird beschrieben, wie Sie Probleme im Zusammenhang mit SMB Multichannel beheben.

## <a name="check-the-network-interface-status"></a>Überprüfen des Status der Netzwerkschnittstelle

Stellen Sie sicher, dass die Bindung für die Netzwerkschnittstelle auf **True** dem SMB-Client (MS \_ -Client) und auf dem SMB-Server (MS-Server) auf true festgelegt ist \_ . Wenn Sie den folgenden Befehl ausführen, sollte in der **Ausgabe für beide** Netzwerkschnittstellen der Wert **true** angezeigt werden:

```PowerShell
Get-NetAdapterBinding -ComponentID ms_server,ms_msclient
```

Stellen Sie danach sicher, dass die Netzwerkschnittstelle in der Ausgabe der folgenden Befehle aufgeführt ist:

```PowerShell
Get-SmbServerNetworkInterface
```

```PowerShell
Get-SmbClientNetworkInterface
```

Sie können auch den **Get-netadapter** -Befehl ausführen, um den Schnittstellen Index anzuzeigen, um das Ergebnis zu überprüfen. Der Schnittstellen Index zeigt alle aktiven SMB-Adapter an, die aktiv an die entsprechende Schnittstelle gebunden sind.

## <a name="check-the-firewall"></a>Überprüfen der Firewall

Wenn nur eine Verbindungs lokale IP-Adresse und keine öffentlich Routing fähige Adresse vorhanden ist, wird das Netzwerk Profil wahrscheinlich auf **Public**festgelegt. Dies bedeutet, dass SMB in der Firewall standardmäßig blockiert wird.

Der folgende Befehl zeigt, welches Verbindungsprofil verwendet wird. Sie können diese Informationen auch mit dem Netzwerk-und Freigabe Center abrufen.

**Get-netconnectionprofile**

Überprüfen Sie in der **Datei-und Druckerfreigabe** Gruppe die Regeln für eingehende Firewall-Regeln, um sicherzustellen, dass "SMB-in" für das korrekte Profil aktiviert ist.

![SMB-in-Regeln](media/smb-multichannel-troubleshooting-1.png)

Sie können auch die **Datei-und Druckerfreigabe** im Fenster **Netzwerk-und Freigabe Center** aktivieren. Wählen Sie hierzu im Menü auf der linken Seite die Option **Erweiterte Freigabe Einstellungen ändern** aus, und wählen Sie dann **Datei-und Druckerfreigabe** für das Profil aktivieren aus. Diese Option aktiviert die Datei-und Druckerfreigabe für Firewallregeln.

![Erweiterte Freigabeeinstellungen ändern](media/smb-multichannel-troubleshooting-2.png)

## <a name="capture-client-and-server-sided-traffic-for-troubleshooting"></a>Erfassen von Client-und Server seitigem Datenverkehr zur Problembehandlung

Sie benötigen die Informationen zur Ablauf Verfolgung für die SMB-Verbindung, die vom TCP-drei-Wege-Handshake gestartet werden Es wird empfohlen, vor dem Start der Erfassung alle Anwendungen (vor allem Windows-Explorer) zu schließen. Starten Sie den Arbeitsstations Dienst auf dem SMB-Client neu, starten **Sie die Paket** Erfassung, und reproduzieren Sie das Problem.

Stellen Sie sicher, dass die SMBv3.*x* -Verbindung ausgehandelt wird und dass sich nichts zwischen dem Server und dem Client auf die Dialekt Aushandlung auswirkt. SMBv2 und frühere Versionen unterstützen Multichannel nicht.

Suchen Sie nach den Netzwerk \_ Schnittstellen \_ Info-Paketen. An dieser Stelle fordert der SMB-Client eine Liste von Adaptern vom SMB-Server an. Wenn diese Pakete nicht ausgetauscht werden, funktioniert Multichannel nicht.

Der Server antwortet, indem er eine Liste gültiger Netzwerkschnittstellen zurückgibt. Der SMB-Client fügt diese dann der Liste der verfügbaren Adapter für Multichannel hinzu. An diesem Punkt sollte Multichannel beginnen und zumindest versuchen, die Verbindung zu starten.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [3.2.4.20.10 Anwendungsanforderungen Abfragen von Netzwerkschnittstellen des Servers](/openspecs/windows_protocols/ms-smb2/147adde4-d936-4597-924a-8caa3429c6b0)

- [2.2.32.5 Netzwerk \_ Schnittstellen \_ Info-Antwort](/openspecs/windows_protocols/ms-smb2/fcd862d1-1b85-42df-92b1-e103199f531f)

- [3.2.5.14.11 behandeln von Netzwerkschnittstellen Antworten](/openspecs/windows_protocols/ms-smb2/5459722b-1eaa-4ead-b465-284363264cad)

In den folgenden Szenarien kann ein Adapter nicht verwendet werden:

- Auf dem Client ist ein Routing Problem aufgetreten. Dies wird in der Regel durch eine falsche Routing Tabelle verursacht, die den Datenverkehr über die falsche Schnittstelle erzwingt.

- Multichannel-Einschränkungen wurden festgelegt. Weitere Informationen finden Sie unter [New-smbmultichanneleinschränkung](/powershell/module/smbshare/new-smbmultichannelconstraint).

- Die Anforderungs-und Antwort Pakete der Netzwerkschnittstelle wurden blockiert.

- Der Client und der Server können nicht über die zusätzliche Netzwerkschnittstelle kommunizieren. Der drei-Wege-Handshake von TCP ist beispielsweise fehlgeschlagen, die Verbindung wird durch eine Firewall blockiert, das Sitzungs Setup ist fehlgeschlagen usw.

Wenn sich der Adapter und seine IPv6-Adresse in der vom Server gesendeten Liste befinden, besteht der nächste Schritt darin, zu überprüfen, ob die Kommunikation über diese Schnittstelle versucht wird. Filtern Sie die Ablauf Verfolgung nach der Link-Local-Adresse und dem SMB-Datenverkehr, und suchen Sie nach einem Verbindungsversuch. Wenn dies eine NetConnection-Ablauf Verfolgung ist, können Sie auch Windows Filter Platform (WFP)-Ereignisse überprüfen, um festzustellen, ob die Verbindung blockiert wird.
