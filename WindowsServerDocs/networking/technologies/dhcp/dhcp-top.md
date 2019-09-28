---
title: Dynamic Host Configuration-Protokoll (DHCP)
description: Dieses Thema enthält eine kurze Übersicht über das Dynamic Host Configuration-Protokoll (DHCP) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 0ff29ef3-c458-4432-9065-e50a7de5b4b9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c71517bc742cf9eda62cc7d83128f1ab9bd04547
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355396"
---
# <a name="dynamic-host-configuration-protocol-dhcp"></a>Dynamic Host Configuration-Protokoll (DHCP)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema finden Sie eine kurze Übersicht über DHCP in Windows Server 2016.

> [!NOTE]
> Zusätzlich zu diesem Thema ist die folgende DHCP-Dokumentation verfügbar.
>
> - [Neues in DHCP](What-s-New-in-DHCP.md)
> - [Bereitstellen von DHCP mithilfe von Windows PowerShell](dhcp-deploy-wps.md)

Das Dynamic Host Configuration-Protokoll (DHCP) ist ein Client/Server-Protokoll, das automatisch einen IP-Host (Internet Protocol) mit seiner IP-Adresse und andere zugehörige Konfigurationsinformationen (z. b. Subnetzmaske und Standard Gateway) bereitstellt. RFCs 2131 und 2132 definieren Sie DHCP als IETF-Standard (Internet Engineering Task Force) basierend auf Bootstrap-Protokoll (BOOTP), einem Protokoll, mit dem DHCP viele Implementierungsdetails gemeinsam nutzt. Mithilfe von DHCP können Hosts erforderliche TCP/IP-Konfigurationsinformationen von einem DHCP-Server abrufen.

Windows Server 2016 umfasst DHCP-Server, eine optionale Netzwerk Server Rolle, die Sie in Ihrem Netzwerk bereitstellen können, um IP-Adressen und andere Informationen an DHCP-Clients zu leasen. Alle Windows-basierten Client Betriebssysteme enthalten den DHCP-Client als Teil von TCP/IP, und der DHCP-Client ist standardmäßig aktiviert.

## <a name="why-use-dhcp"></a>Gründe für die Verwendung von DHCP

Jedes Gerät in einem TCP/IP-basierten Netzwerk muss über eine eindeutige Unicast-IP-Adresse für den Zugriff auf das Netzwerk und seine Ressourcen verfügen. Ohne DHCP müssen IP-Adressen für neue Computer oder Computer, die von einem Subnetz zu einem anderen verschoben werden, manuell konfiguriert werden. IP-Adressen für Computer, die aus dem Netzwerk entfernt werden, müssen manuell freigegeben werden.

Mit DHCP wird der gesamte Prozess automatisiert und zentral verwaltet. Der DHCP-Server verwaltet einen Pool von IP-Adressen und leert eine Adresse an einen beliebigen DHCP-fähigen Client, wenn er im Netzwerk gestartet wird. Da die IP-Adressen dynamisch (geleast) und nicht statisch (dauerhaft zugewiesen) sind, werden Adressen, die nicht mehr verwendet werden, automatisch zur erneuten Zuordnung an den Pool zurückgegeben.

Der Netzwerkadministrator richtet DHCP-Server ein, die TCP/IP-Konfigurationsinformationen verwalten, und stellt die Adress Konfiguration für DHCP-fähige Clients in Form eines Lease-Angebots bereit. Der DHCP-Server speichert die Konfigurationsinformationen in einer Datenbank, die Folgendes enthält:

- Gültige TCP/IP-Konfigurationsparameter für alle Clients im Netzwerk.

- Gültige IP-Adressen, die in einem Pool für die Zuweisung an Clients verwaltet werden, sowie ausgeschlossene Adressen.

- Reservierte IP Adressen, die bestimmten DHCP-Clients zugeordnet sind. Dies ermöglicht eine konsistente Zuweisung einer einzelnen IP-Adresse zu einem einzelnen DHCP-Client.

- Die Leasedauer oder die Zeitspanne, für die die IP-Adresse verwendet werden kann, bevor eine Leaseerneuerung erforderlich ist.

Ein DHCP-fähiger Client empfängt nach Annahme eines Lease-Angebots Folgendes:

- Eine gültige IP-Adresse für das Subnetz, mit dem eine Verbindung hergestellt wird.  
  
- Angeforderte DHCP-Optionen, bei denen es sich um zusätzliche Parameter handelt, die ein DHCP-Server für die Zuweisung zu Clients konfiguriert ist Einige Beispiele für DHCP-Optionen sind Router (Standard Gateway), DNS-Server und DNS-Domänen Name.

## <a name="benefits-of-dhcp"></a>Vorteile von DHCP

DHCP bietet die folgenden Vorteile:

- **Konfiguration der zuverlässigen IP-Adresse**. DHCP minimiert Konfigurationsfehler, die durch die manuelle Konfiguration von IP-Adressen verursacht werden, z. b. typografische Fehler oder Adresskonflikte, die durch die Zuweisung einer IP-Adresse zu mehreren Computern gleichzeitig verursacht werden.

- **Reduzierte Netzwerk Administration**. DHCP umfasst die folgenden Funktionen, um die Netzwerkverwaltung zu reduzieren:

    - Zentralisierte und automatisierte TCP/IP-Konfiguration.

    - Die Möglichkeit, TCP/IP-Konfigurationen von einem zentralen Speicherort aus zu definieren.

    - Die Möglichkeit, mithilfe von DHCP-Optionen einen vollständigen Bereich zusätzlicher TCP/IP-Konfigurationswerte zuzuweisen.

    - Die effiziente Handhabung von IP-Adressänderungen für Clients, die häufig aktualisiert werden müssen, z. b. für tragbare Geräte, die an verschiedene Speicherorte in einem Drahtlos Netzwerk verschoben werden.

    - Die Weiterleitung der anfänglichen DHCP-Nachrichten mithilfe eines DHCP-Relay-Agents. Dadurch entfällt die Notwendigkeit eines DHCP-Servers in jedem Subnetz.

