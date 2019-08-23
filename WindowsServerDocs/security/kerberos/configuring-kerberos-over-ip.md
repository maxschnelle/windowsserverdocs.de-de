---
title: Konfigurieren von Kerberos für die IP-Adresse
description: Kerberos-Unterstützung für IP-basierte SPNs
author: daveba
ms.author: daveba
ms.openlocfilehash: 1061364528100fe005e80f64c6315f9fca69ad98
ms.sourcegitcommit: 2082335e1260826fcbc3dccc208870d2d9be9306
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69980298"
---
# <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos-Clients lassen IPv4-und IPv6-Adress Hostnamen in Dienst Prinzipal Namen (SPNs) zu.

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Ab Windows 10, Version 1507 und Windows Server 2016, können Kerberos-Clients für die Unterstützung von IPv4-und IPv6-Hostnamen in SPNs konfiguriert werden.

Standardmäßig versucht Windows nicht, die Kerberos-Authentifizierung für einen Host durchführen, wenn der Hostname eine IP-Adresse ist. Es wird auf andere aktivierte Authentifizierungsprotokolle wie NTLM zurückgegriffen. Anwendungen sind jedoch manchmal hart codiert, um IP-Adressen zu verwenden. Dies bedeutet, dass die Anwendung auf NTLM zurückgreift und nicht Kerberos verwendet. Dies kann zu Kompatibilitätsproblemen führen, wenn Umgebungen zum Deaktivieren von NTLM verschoben werden.

Um die Auswirkung der Deaktivierung von NTLM zu reduzieren, wurde eine neue Funktion eingeführt, die es Administratoren ermöglicht, IP-Adressen als Hostnamen in Dienst Prinzipal Namen zu verwenden. Diese Funktion wird auf dem Client über einen Registrierungsschlüssel Wert aktiviert.

```cmd
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters" /v TryIPSPN /t REG_DWORD /d 1 /f
```

Erstellen Sie einen tryipspn-Eintrag, um die Unterstützung für IP-Adress Hostnamen in SPNs zu konfigurieren. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert in 1. Dieser Registrierungs Wert muss auf jedem Client Computer festgelegt werden, der über die IP-Adresse auf durch Kerberos geschützte Ressourcen zugreifen muss.

## <a name="configuring-a-service-principal-name-as-ip-address"></a>Konfigurieren eines Dienst Prinzipal namens als IP-Adresse

Ein Dienst Prinzipal Name ist ein eindeutiger Bezeichner, der während der Kerberos-Authentifizierung zum Identifizieren eines Dienstanbieter verwendet wird. Ein SPN besteht aus einem Dienst, einem Hostnamen und optional einem Port in Form von `service/hostname[:port]` , wie `host/fs.contoso.com`z. b. Windows registriert mehrere SPNs bei einem Computer Objekt, wenn ein Computer mit Active Directory verknüpft ist.

IP-Adressen werden normalerweise nicht anstelle von Hostnamen verwendet, da IP-Adressen häufig temporär sind. Dies kann zu Konflikten und Authentifizierungs Fehlern führen, wenn Adressleases ablaufen und erneuert werden. Daher ist die Registrierung eines auf IP-Adressen basierenden SPN ein manueller Prozess und sollte nur verwendet werden, wenn es unmöglich ist, zu einem DNS-basierten Hostnamen zu wechseln.

Die empfohlene Vorgehensweise ist die Verwendung des Tools [Setspn. exe](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)) . Beachten Sie, dass ein SPN nur für ein einzelnes Konto in Active Directory registriert werden kann, daher wird empfohlen, dass IP-Adressen bei Verwendung von DHCP statische Leases aufweisen.

```
Setspn -s <service>/ip.address> <domain-user-account>  
```

Beispiel:

```
Setspn -s host/192.168.1.1 server01
```
