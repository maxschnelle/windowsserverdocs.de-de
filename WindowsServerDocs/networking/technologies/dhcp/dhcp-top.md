---
title: Dynamic Host Configuration-Protokoll (DHCP)
description: Dieses Thema enthält eine kurze Übersicht über die von Dynamic Host Configuration Protokoll (DHCP) in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: article
ms.assetid: 0ff29ef3-c458-4432-9065-e50a7de5b4b9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 770cfd78c7b9a0e122bd9f9936623a73b56af808
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="dynamic-host-configuration-protocol-dhcp"></a>Dynamic Host Configuration-Protokoll (DHCP)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können eine kurze Übersicht über DHCP in Windows Server2016.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgende DHCP-Dokumentation verfügbar.
>
>- [Neues in DHCP](What-s-New-in-DHCP.md)
>- [Bereitstellen von DHCP mit der WindowsPowerShell](dhcp-deploy-wps.md)

Dynamic Host Configuration-Protokoll (DHCP) ist ein Client/Server-Protokoll, das automatisch einen Host IP (Internet Protocol) mit der IP-Adresse und andere Konfigurationsinformationen, z.B. die Subnetzmaske und das Standardgateway. In den RFCs 2131 und 2132 definieren Sie DHCP als ein Internet Engineering Task Force (IETF) Standard basierend auf Bootstrap Protokoll (BOOTP), ein Protokoll, mit denen DHCP viele Implementierungsdetails teilt. DHCP ermöglicht Hosts von einem DHCP-Server erforderlichen TCP/IP-Konfigurationsinformationen abzurufen.

Windows Server2016 enthält DHCP-Server eine optionale Netzwerk Serverrolle ist, die Sie auf das Netzwerk für die IP-Adressleases und andere Informationen zu DHCP-Clients bereitstellen können. Alle Windows-basierter Client-Betriebssysteme enthalten den DHCP-Client als Teil des TCP/IP und DHCP-Client ist standardmäßig aktiviert.

## <a name="why-use-dhcp"></a>Gründe für die Verwendung von DHCP

Jedes Gerät in einem TCP/IP-basierten Netzwerk muss eine eindeutige Unicast-IP-Adresse den Zugriff auf das Netzwerk und seine Ressourcen verfügen. Ohne DHCP müssen IP-Adressen für neue Computer oder für Computer, die aus einem Subnetz auf einen anderen verschoben werden manuell konfiguriert werden; IP-Adressen für Computer, die aus dem Netzwerk entfernt werden, müssen manuell freigegeben werden.

Mit DHCP wird das gesamte Verfahren automatisiert und zentral verwaltet. Der DHCP-Server verwaltet einen Pool von IP-Adressen und verleiht eine Adresse an alle DHCP-fähige Clients, wenn es im Netzwerk startet. Da die IP-Adressen dynamisch sind (geleasten), statt statische (dauerhaft zugewiesen), werden Adressen nicht mehr in der automatisch dem Pool zur erneuten Belegung zurückgegeben.

Der Netzwerkadministrator erstellt DHCP-Servern, die die TCP/IP-Konfigurationsinformationen verwalten und Konfiguration der Adresse für DHCP-fähige Clients in Form von angebotene Lease an. Der DHCP-Server werden die Konfigurationsinformationen in einer Datenbank, die enthält:

- Gültige TCP/IP-Konfigurationsparameter für alle Clients im Netzwerk.

- Gültige IP-Adressen in einem Pool für die Zuweisung an Clients verwaltet, sowie Adressen ausgeschlossen.

- Reservierte IP-Adressen bestimmter DHCP-Clients zugeordnet. Dies ermöglicht eine einheitliche Zuweisung einer IP-Adresse für einen einzelnen DHCP-Client.

- Die Leasedauer, oder die Zeitspanne, für die die IP-Adresse verwendet werden kann, bevor eine Leaseerneuerung erforderlich ist.

Ein DHCP-fähige Client, auf eine Lease-Angebot akzeptiert wird:

- Eine gültige IP-Adresse für das Subnetz, zu dem eine Verbindung hergestellt wird.  
  
- DHCP-Optionen, zusätzliche Parameter, die ein DHCP-Server konfiguriert ist angefordert Clients zuweisen. Einige Beispiele für DHCP-Optionen sind Router (Standardgateway), DNS-Server und DNS-Domänennamen.

## <a name="benefits-of-dhcp"></a>Vorteile von DHCP

DHCP bietet folgende Vorteile.

- **Zuverlässige IP-Adresskonfiguration**. DHCP Konfigurationsfehler durch manuelle IP-Adresskonfiguration, z.B. Rechtschreibfehler, minimiert oder -Konflikte zurückzuführen, dass die Zuweisung von IP-Adresse für mehrere Computer gleichzeitig.

- **Reduzierte Netzwerkadministration**. DHCP umfasst die folgenden Features aus, um die Netzwerkadministration reduzieren:

    - Zentralisierte und automatisierte TCP/IP-Konfiguration.

    - Die Möglichkeit, TCP/IP-Konfigurationen von einem zentralen Ort zu definieren.

    - Die Möglichkeit, eine Vielzahl von zusätzlichen TCP/IP-Konfigurationswerte durch DHCP-Optionen zugewiesen.

    - Effiziente Behandlung der IP-Adresse wird für Clients, die häufig, z.B. für tragbare Geräte aktualisiert werden müssen, die an andere Speicherorte in einem Drahtlosnetzwerk zu verschieben.

    - Die Weiterleitung der ursprünglichen DHCP-Nachrichten mit einem DHCP-Relay-Agent, der ein DHCP-Server in jedem Subnetz überflüssig.

