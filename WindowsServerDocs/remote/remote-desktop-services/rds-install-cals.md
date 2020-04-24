---
title: Installieren von RDS-Clientzugriffslizenzen
description: Hier erfährst du, wie du Clientzugriffslizenzen (Client Access Licenses, CALs) für Remotedesktopclients installierst.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: 3a9f73418bd4da67c97db30a3272588afc287b95
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80860443"
---
# <a name="install-rds-client-access-licenses-on-the-remote-desktop-license-server"></a>Installieren von RDS-Clientzugriffslizenzen auf dem Remotedesktop-Lizenzserver

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Verwende die folgenden Informationen, um Clientzugriffslizenzen für Remotedesktopdienste (RDS-CALs) auf dem Remotedesktop-Lizenzserver zu installieren. Sobald die CALs installiert sind, stellt der Lizenzserver diese nach Bedarf für Benutzer aus.

Beachte, dass du auf dem Computer, auf dem der Remotedesktoplizenzierungs-Manager ausgeführt wird, eine Internetverbindung benötigst, nicht jedoch auf dem Computer, auf dem der Lizenzserver ausgeführt wird.

1. Öffne den Remotedesktoplizenzierungs-Manager auf dem Lizenzserver (in der Regel der erste Remotedesktop-Verbindungsbroker).
2. Klicke mit der rechten Maustaste auf den Lizenzserver, und klicke dann auf **Lizenzen installieren**.
3. Klicke auf der Begrüßungsseite auf **Weiter**.
4. Wähle das Programm aus, über das du deine RDS-CALs erworben hast, und klicke dann auf **Weiter**. Wenn du Dienstanbieter bist, wähle **Dienstanbieter-Lizenzvereinbarung** aus.
5. Gib die Informationen zu deinem Lizenzprogramm ein. In den meisten Fällen handelt es sich hierbei um den Lizenzcode oder eine Vertragsnummer, dies richtet sich jedoch nach dem von dir genutzten Lizenzprogramm.
6. Klicken Sie auf **Weiter**.
7. Wähle die Produktversion, den Lizenztyp und die Anzahl von Lizenzen für deine Umgebung aus, und klicke dann auf **Weiter**. Der Lizenz-Manager kontaktiert das Microsoft Clearinghouse, um deine Lizenzen zu überprüfen und abzurufen.
8.  Klicken Sie auf **Fertig stellen**, um den Vorgang abzuschließen.