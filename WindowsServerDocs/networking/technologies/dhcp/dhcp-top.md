---
title: Dynamic Host Configuration-Protokoll (DHCP)
description: Dieses Thema enthält eine kurze Übersicht des Dynamic Host Configuration Protocol (DHCP), in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 0ff29ef3-c458-4432-9065-e50a7de5b4b9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 08b07e902486ae633b30949270e15f8bf94afaaf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857491"
---
# <a name="dynamic-host-configuration-protocol-dhcp"></a>Dynamic Host Configuration-Protokoll (DHCP)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema für einen kurzen Überblick über DHCP unter Windows Server 2016 verwenden.

>[!NOTE]
>Zusätzlich zu diesem Thema wird die folgende Dokumentation zum DHCP-verfügbar.
>
>- [Neues in DHCP](What-s-New-in-DHCP.md)
>- [Bereitstellen von DHCP mit Windows PowerShell](dhcp-deploy-wps.md)

Dynamic Host Configuration Protocol (DHCP) ist ein Client/Server-Protokoll, das einen Host IP (Internet Protocol) automatisch mit der IP-Adresse und andere verwandte Konfigurationsinformationen wie z. B. die Subnetzmaske und das Standard-Gateway bereitstellt. RFC 2131 und 2132 definieren DHCP als ein Internet Engineering Task Force (IETF) standard basierend auf Bootstrapprotokoll (BOOTP), ein Protokoll, mit denen viele Implementierungsdetails von DHCP teilt. DHCP ermöglicht Hosts das Abrufen von erforderlichen TCP/IP-Konfigurationsinformationen von DHCP-Server.

Windows Server 2016 enthält DHCP-Server, der eine optionale networking-Serverrolle, die Sie für Ihr Netzwerk für die IP-Adressleases und Weitere Informationen zum DHCP-Clients bereitstellen können. Alle Windows-basierten Client-Betriebssysteme enthalten den DHCP-Client als Teil des TCP/IP und DHCP-Client ist standardmäßig aktiviert.

## <a name="why-use-dhcp"></a>Gründe für die Verwendung von DHCP

Jedes Gerät in einem TCP/IP-basierten Netzwerk müssen eine eindeutige Unicast IP-Adresse im Netzwerk und seine Ressourcen zugreifen. Ohne DHCP müssen die IP-Adressen für neue Computer oder Computer, die aus einem Subnetz in ein anderes verschoben werden manuell konfiguriert werden; IP-Adressen für Computer, die aus dem Netzwerk entfernt werden, müssen manuell freigegeben werden.

Mit DHCP wird der gesamte Prozess automatisiert und zentral verwaltet. Der DHCP-Server verwaltet einen Pool mit IP-Adressen und eine Adresse für andere DHCP-fähigen Clients geleast, wenn es im Netzwerk wird gestartet. Da die IP-Adressen dynamisch sind (geleast), statt statisch (dauerhaft zugewiesen), werden nicht mehr verwendeten Adressen automatisch an den Pool für die neuzuordnung zurückgegeben.

Der Netzwerkadministrator richtet ein DHCP-Servern, die TCP/IP-Konfigurationsinformationen verwalten und Konfigurieren der Adresse für DHCP-fähigen Clients in Form von als Lease angeboten. Der DHCP-Server speichert die Konfigurationsinformationen in einer Datenbank, die enthält:

- Gültige TCP/IP-Konfigurationsparameter für alle Clients im Netzwerk.

- Gültige IP-Adressen, verwaltet, die in einem Pool für die Zuweisung an Clients als auch Adressen ausgeschlossen.

- Reservierte IP-Adressen bestimmten DHCP-Clients. Dies ermöglicht eine konsistente Zuweisung einer einzelnen IP-Adresse für einen einzelnen DHCP-Client.

- Die Leasedauer, oder die Zeitspanne, die für die die IP-Adresse verwendet werden kann, bevor die Erneuerung einer Lease erforderlich ist.

Ein DHCP-fähigen Client, auf die als Lease angeboten, akzeptieren erhält:

- Eine gültige IP-Adresse für das Subnetz, das sie eine Verbindung herstellt.  
  
- Angefordert von DHCP-Optionen, mit denen zusätzliche Parameter, der auf ein DHCP-Server konfiguriert ist, sind Clients zuweisen. Einige Beispiele für die DHCP-Optionen sind Router (Standardgateway), DNS-Server und DNS-Domänennamen an.

## <a name="benefits-of-dhcp"></a>Vorteile von DHCP

DHCP bietet folgende Vorteile.

- **Zuverlässige IP-Adresskonfiguration**. DHCP wird durch manuelle Konfiguration IP-Adresse, z. B. Rechtschreibfehler, verursacht Konfigurationsfehler minimiert oder durch die Zuweisung einer IP-Adresse auf mehrere Computer gleichzeitig verursachten Konflikte zu beheben.

- **Reduziert die Netzwerkadministration**. DHCP umfasst die folgenden Funktionen aus, um die Netzwerkadministration zu reduzieren:

    - Zentralisierte und automatisierte TCP/IP-Konfiguration.

    - Die Fähigkeit, TCP/IP-Konfigurationen von einem zentralen Ort zu definieren.

    - Die Möglichkeit, zahlreiche weitere Werte von TCP/IP-Konfiguration mithilfe von DHCP-Optionen zugewiesen werden soll.

    - Effiziente Behandlung der IP-Adressänderungen für Clients, die häufig, z. B. für tragbare Geräte aktualisiert werden muss, die an unterschiedliche Positionen in einem drahtlosen Netzwerk zu verschieben.

    - Die Weiterleitung der anfänglichen DHCP-Nachrichten mithilfe eines DHCP-Relay-Agents, der entfällt die Notwendigkeit von einem DHCP-Server auf jedem Subnetz.

