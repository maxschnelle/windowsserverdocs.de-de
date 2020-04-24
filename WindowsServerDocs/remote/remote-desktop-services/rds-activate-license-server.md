---
title: Aktivieren des Remotedesktopdienste-Lizenzservers
description: Installieren und Aktivieren des RD-Lizenzservers
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.topic: article
ms.assetid: eb24ddd2-0361-41fe-bd6b-c7c63427cb71
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: 3eaa999c03c97ad3188d4dcd8514b2705bf0a3b1
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80852973"
---
# <a name="activate-the-remote-desktop-services-license-server"></a>Aktivieren des Remotedesktopdienste-Lizenzservers

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Der Remotedesktopdienste-Lizenzserver gibt Clientzugriffslizenzen (Client Access Licenses, CALs) für Benutzer und Geräte aus, wenn diese auf den RD-Sitzungshost zugreifen. Du kannst den Lizenzserver mit dem Remotedesktoplizenzierungs-Manager aktivieren. 

## <a name="install-the-rd-licensing-role"></a>Installieren der Rolle „Remotedesktoplizenzierung“

1. Melde dich mit einem Administratorkonto bei dem Server an, den du als Lizenzserver verwenden möchtest.
2. Klicke im Server-Manager auf **Rollenübersicht** und dann auf **Rollen hinzufügen**.
   Klicke auf der ersten Seite des Rollen-Assistenten auf **Weiter**.
3. Wähle **Remotedesktopdienste** aus, und klicke dann auf **Weiter** und auf der Seite für Remotedesktopdienste ebenfalls auf **Weiter**.
4. Wähle **Remotedesktoplizenzierung** aus, und klicke dann auf **Weiter**.
5. Konfiguriere die Domäne: Wähle **Konfigurieren eines Suchbereichs für diesen Lizenzserver** aus, und klicke auf **Diese Domäne** und dann auf **Weiter**.
6. Klicken Sie auf **Installieren**.

## <a name="activate-the-license-server"></a>Aktivieren des Lizenzservers

1. Öffne den Remotedesktoplizenzierungs-Managers: Klicke auf **Start > Verwaltung > Remotedesktopdienste > Remotedesktoplizenzierungs-Manager**.
2. Klicke mit der rechten Maustaste auf den Lizenzserver, und klicke dann auf **Server aktivieren**.
3. Klicke auf der Startseite auf **Weiter**.
4. Wähle als Verbindungsmethode die Option **Automatische Verbindung (empfohlen)** aus, und klicke dann auf **Weiter**.
5. Gib die Unternehmensinformationen (deinen Namen, den Unternehmensnamen, deine geografische Region) ein, und klicke dann auf **Weiter**.
6. Gib optional weitere Unternehmensinformationen (etwa E-Mail-Adresse und Unternehmensadresse) ein,und klicke dann auf**Weiter**. 
7. Stelle sicher, dass **Assistent für die Lizenzinstallation starten** nicht ausgewählt ist. (Wir installieren die Lizenzen später.) Klicke dann auf **Weiter**.

Der Lizenzserver kann jetzt zum Ausstellen und Verwalten von Lizenzen verwendet werden. 