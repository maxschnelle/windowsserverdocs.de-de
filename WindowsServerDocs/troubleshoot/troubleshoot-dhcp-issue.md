---
title: Handbuch zur Problembehandlung für das Dynamic Host Configuration-Protokoll (DHCP)
description: Diese Artilce enthält eine Anleitung zur Problembehandlung für DHCP-Probleme.
manager: dcscontentpm
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: 92a7984fe2070ac194aa01a5a9aa63e85b7aa45d
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078617"
---
# <a name="troubleshooting-guide-for-dynamic-host-configuration-protocol-dhcp"></a>Handbuch zur Problembehandlung für das Dynamic Host Configuration-Protokoll (DHCP)

Damit jedes Gerät (z. b. ein Computer oder Telefon) in einem Netzwerk betrieben werden kann, muss ihm eine IP-Adresse zugewiesen werden. Sie können eine IP-Adresse manuell oder automatisch zuweisen. Die automatische Zuweisung erfolgt durch den DHCP-Dienst (Microsoft-oder Drittanbieter Server).

In diesem Artikel werden allgemeine Schritte zur Problembehandlung für den Microsoft IPv4 DHCP-Client und-Server erläutert.

## <a name="more-information"></a>Weitere Informationen

Die Prozedur für die IPv4-Adresszuweisung umfasst in der Regel drei Hauptkomponenten:

- Ein DHCP-Client Gerät, das eine IP-Adresse abrufen muss

- Ein DHCP-Dienst, der auf der Grundlage bestimmter Einstellungen IP-Adressen für den Client bereitstellt.

- Ein DHCP-Relay-Agent/IP Helper zum Senden von DHCP-Broadcast Anforderungen an ein anderes Netzwerksegment

Die Kommunikation zwischen DHCP-Client und Server besteht aus drei Arten der Interaktion zwischen den beiden Peers:

- **Broadcast basierte Dora** (ermitteln, Angebot, Anforderung, Bestätigung). Dieser Vorgang umfasst die folgenden Schritte:

    - Der DHCP-Client sendet eine DHCP Discovery-Broadcast Anforderung an alle verfügbaren DHCP-Server innerhalb des gültigen Bereichs.

    - Eine DHCP-Angebot-Broadcast Antwort wird vom DHCP-Server empfangen und bietet eine verfügbare IP-Adresse.

    - Die DHCP-Client Broadcast Anforderung fordert am Ende die angebotene IP-Adress Lease und die DHCP-Broadcast Bestätigung an.

    - Wenn sich der DHCP-Client und-Server in unterschiedlichen logischen Netzwerksegmenten befinden, wird von einem DHCP-Relay-Agent eine Weiterleitung durchlaufen, und die DHCP-Broadcast Pakete werden zwischen Peers hin und her gesendet.

- **Unicastdhcp**-Erneuerungs Anforderungen: Diese werden direkt vom DHCP-Client an den DHCP-Server gesendet, um die IP-Adresszuweisung nach 50 Prozent der IP-Adress Lease zu erneuern.

- **Neubinden von DHCP-Broadcast Anforderungen**: Diese werden an jeden DHCP-Server innerhalb des Bereichs des Clients vorgenommen. Diese werden nach 87,5 Prozent der IP-Adress Leasedauer gesendet, da dies darauf hinweist, dass die gesteuerte unicastanforderung nicht funktioniert hat. Wie beim Dora-Prozess umfasst dieser Prozess die Kommunikation mit dem DHCP-Relay-Agent.

Wenn ein Microsoft DHCP-Client keine gültige DHCP-IPv4-Adresse erhält, ist der Client wahrscheinlich für die Verwendung einer APIPA-Adresse konfiguriert. Weitere Informationen finden Sie im folgenden Knowledge Base-Artikel: [220874](https://support.microsoft.com/help/220874) verwenden der automatischen TCP/IP-Adressierung ohne DHCP-Server.

Die gesamte Kommunikation erfolgt über UDP-Ports 67 und 68. Weitere Informationen finden Sie im folgenden Knowledge Base-Artikel: [169289](https://support.microsoft.com/help/169289) DHCP (Dynamic Host Configuration-Protokoll) Grundlagen.