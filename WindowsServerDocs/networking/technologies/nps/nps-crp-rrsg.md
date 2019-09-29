---
title: RADIUS-Remoteservergruppen
description: Dieses Thema enthält eine Übersicht über die Remote-RADIUS-Server Gruppen für den Netzwerk Richtlinien Server in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d81678a7-be21-48f2-9b3f-5a75d6aef013
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 63a6eb5f0f78ed8dbcc0144602f16274fd6ec213
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396312"
---
# <a name="remote-radius-server-groups"></a>RADIUS-Remoteservergruppen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie den Netzwerk Richtlinien Server (Network Policy Server, NPS) als RADIUS-Proxy (Remote Authentication Dial-in User Service) konfigurieren, verwenden Sie NPS, um Verbindungsanforderungen an RADIUS-Server weiterzuleiten, die die Verbindungsanforderungen verarbeiten können, da Sie Authentifizierung und Autorisierung in der Domäne, in der sich das Benutzer-oder Computer Konto befindet. Wenn Sie z. b. Verbindungsanforderungen an einen oder mehrere RADIUS-Server in nicht vertrauenswürdigen Domänen weiterleiten möchten, können Sie NPS als RADIUS-Proxy konfigurieren, um die Anforderungen an die Remote-RADIUS-Server in der nicht vertrauenswürdigen Domäne weiterzuleiten.

>[!NOTE]
>Remote-RADIUS-Server Gruppen sind von Windows-Gruppen unabhängig voneinander getrennt.

Wenn Sie NPS als RADIUS-Proxy konfigurieren möchten, müssen Sie eine Verbindungs Anforderungs Richtlinie erstellen, die alle Informationen enthält, die erforderlich sind, damit NPS auswerten kann, welche Nachrichten weiterleiten und wohin die Nachrichten gesendet werden sollen.

Wenn Sie eine RADIUS-Remote Server Gruppe in NPS konfigurieren und eine Verbindungs Anforderungs Richtlinie mit der Gruppe konfigurieren, legen Sie den Speicherort fest, an dem NPS Verbindungsanforderungen weiterleiten soll.

## <a name="configuring-radius-servers-for-a-group"></a>Konfigurieren von RADIUS-Servern für eine Gruppe

Eine Remote-RADIUS-Server Gruppe ist eine benannte Gruppe, die einen oder mehrere RADIUS-Server enthält. Wenn Sie mehr als einen Server konfigurieren, können Sie die Einstellungen für den Lastenausgleich festlegen, um entweder die Reihenfolge zu bestimmen, in der die Server vom Proxy verwendet werden, oder den Fluss von RADIUS-Nachrichten auf allen Servern in der Gruppe zu verteilen, um zu verhindern, dass mindestens ein Server überladen wird. mit zu vielen Verbindungsanforderungen.

Jeder Server in der Gruppe weist die folgenden Einstellungen auf.

- Der **Name oder die Adresse**. Jedes Gruppenmitglied muss innerhalb der Gruppe über einen eindeutigen Namen verfügen. Der Name kann eine IP-Adresse oder ein Name sein, der in seine IP-Adresse aufgelöst werden kann.

- **Authentifizierung und Kontoführung**. Sie können Authentifizierungsanforderungen, Buchhaltungs Anforderungen oder beides an jedes Mitglied der RADIUS-Remote Server Gruppe weiterleiten.

- **Lastenausgleich**. Eine Prioritäts Einstellung wird verwendet, um anzugeben, welches Mitglied der Gruppe der primäre Server ist (die Priorität ist auf 1 festgelegt). Für Gruppenmitglieder mit der gleichen Priorität wird eine Gewichtungs Einstellung verwendet, um zu berechnen, wie oft RADIUS-Nachrichten an die einzelnen Server gesendet werden. Sie können zusätzliche Einstellungen verwenden, um die Art und Weise zu konfigurieren, in der der NPS erkennt, wenn ein Gruppenmitglied zum ersten Mal nicht mehr verfügbar ist, und wenn es verfügbar ist, wenn es als nicht verfügbar eingestuft wird.

Nachdem Sie eine Remote-RADIUS-Server Gruppe konfiguriert haben, können Sie die Gruppe in den Authentifizierungs-und Kontoführungs Einstellungen einer Verbindungs Anforderungs Richtlinie angeben. Aus diesem Grund können Sie zuerst eine Remote-RADIUS-Server Gruppe konfigurieren. Als nächstes können Sie die Verbindungs Anforderungs Richtlinie so konfigurieren, dass die neu konfigurierte Remote-RADIUS-Server Gruppe verwendet wird. Alternativ können Sie den Assistenten für neue Verbindungs Anforderungs Richtlinien verwenden, um eine neue Remote-RADIUS-Server Gruppe zu erstellen, während Sie die Verbindungs Anforderungs Richtlinie erstellen.

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).
