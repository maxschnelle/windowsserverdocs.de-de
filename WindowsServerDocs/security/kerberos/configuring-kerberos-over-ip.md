---
title: Konfigurieren von Kerberos für die IP-Adresse
description: Kerberos-Unterstützung für IP-basierte SPNs
ms.openlocfilehash: aa2685fcff2fdf231e5e5884d25885585f0bd6c9
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67279968"
---
# <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos-Clients zulassen IPv4 und IPv6-Adresse-Hostnamen in Service Principal Names (SPNs)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Ab Windows 10 Version 1507 und Windows Server 2016, können Kerberos-Clients konfiguriert werden, zur Unterstützung von IPv4 und IPv6-Hostnamen in SPNs.

Standardmäßig wird Windows Kerberos-Authentifizierung für einen Host nicht versuchen, wenn der Hostname eine IP-Adresse ist. Mit anderen Protokollen der aktivierten Authentifizierungsoptionen wie NTLM wird zurückgegriffen. Anwendungen sind jedoch manchmal hartcodierte IP-Adressen verwenden, das bedeutet, die Anwendung dass auf NTLM zurückgegriffen wird, und Kerberos nicht verwendet. Dies kann Kompatibilitätsprobleme verursachen, wenn Umgebungen verschieben, um NTLM zu deaktivieren.

Zur Reduzierung der Auswirkungen einer Deaktivierung von NTLM eine neue Funktion wurde eingeführt, die Administratoren, die IP-Adressen als Hostnamen im Service Principal Names verwenden können. Diese Funktion ist auf dem Client über einen Wert des Registrierungsschlüssels aktiviert.

```cmd
reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters" /v TryIPSPN /t REG_DWORD /d 1 /f
```

Erstellen Sie einen TryIPSPN-Eintrag, um Unterstützung für IP-Adresse Hostnamen in SPNs zu konfigurieren. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Nachdem Sie den Eintrag erstellt haben, ändern Sie den DWORD-Wert auf 1 fest. Dieser Registrierungswert auf jedem Clientcomputer, die Zugriff auf Kerberos-geschützten Ressourcen über die IP-Adresse festgelegt werden müssen.

## <a name="configuring-a-service-principal-name-as-ip-address"></a>Konfigurieren eines Dienstprinzipalnamens als IP-Adresse

A Service Principal Name ist ein eindeutiger Bezeichner, die während der Kerberos-Authentifizierung verwendet wird, um einen Dienst im Netzwerk zu identifizieren. Ein SPN besteht aus einem Dienst, Hostnamen und optional einen Port in Form von `service/hostname[:port]` wie z. B. `host/fs.contoso.com`. Windows wird mehrere SPNs, um ein Computerobjekt registriert, wenn ein Computer mit Active Directory verknüpft ist.

IP-Adressen sind normalerweise nicht anstelle von Hostnamen verwendet, da es sich bei IP-Adressen oft temporär sind. Dies kann zu Konflikten und Authentifizierungsfehlern führen, wie Adressleases laufen ab und zu erneuern. Aus diesem Grund registrieren einen IP-Adressen basierenden SPN ist ein manueller Prozess, und sollte nur verwendet werden, wenn es nicht möglich, wechseln Sie auf eine Basis von DNS-Hostname ist.

Der empfohlene Ansatz ist die Verwendung der [Setspn.exe](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)) Tool. Beachten Sie, dass ein SPN nur registriert werden kann, die einem einzelnen Konto in Active Directory zu einem Zeitpunkt daher wird empfohlen, dass die IP-Adressen statisch Leases aufweisen, wenn DHCP verwendet wird.

```
Setspn -s <service>/ip.address> <domain-user-account>  
```

Beispiel:

```
Setspn -s host/192.168.1.1 server01
```
