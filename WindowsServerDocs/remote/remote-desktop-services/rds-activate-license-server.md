---
title: Aktivieren des Lizenzservers Remote Desktop Services
description: Installieren Sie und aktivieren Sie des Remotedesktop-Lizenzservers
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb24ddd2-0361-41fe-bd6b-c7c63427cb71
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: d28ceac9cde0ee2d4c92867bdd90d5c463a8cd4c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888011"
---
# <a name="activate-the-remote-desktop-services-license-server"></a>Aktivieren des Lizenzservers Remote Desktop Services

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Beim Zugriff auf den Remotedesktop-Sitzungshost-Lizenz der Remote Desktop Services Server Probleme-Clientzugriffslizenzen (CALs) für Benutzer und Geräte. Sie können den Lizenzserver aktivieren, indem Sie den Remotedesktoplizenzierungs-Manager. 

## <a name="install-the-rd-licensing-role"></a>Installieren Sie die Rolle "Remotedesktoplizenzierung"

1. Melden Sie sich an den Server, die, den Sie als den Lizenzserver mit einem Administratorkonto verwenden möchten.
2. Klicken Sie im Server-Manager **Rollenübersicht**, und klicken Sie dann auf **Hinzufügen von Rollen**.
   Klicken Sie auf **Weiter** auf der ersten Seite des Assistenten für Rollen.
3. Wählen Sie **Remote Desktop Services**, und klicken Sie dann auf **Weiter**, und klicken Sie dann **Weiter** auf der Seite "Remotedesktopdienste".
4. Wählen Sie **Remotedesktoplizenzierung**, und klicken Sie dann auf **Weiter**.
5. Konfigurieren Sie die Domäne: Wählen Sie **konfigurieren Sie einen Ermittlungsbereich für diesen Lizenzserver**, klicken Sie auf **dieser Domäne**, und klicken Sie dann auf **Weiter**.
6. Klicken Sie auf **Installieren**.

## <a name="activate-the-license-server"></a>Aktivieren des Lizenzservers

1. Öffnen Sie den Remotedesktoplizenzierungs-Manager: Klicken Sie auf **Start > Verwaltung > Remotedesktopdienste > Remotedesktoplizenzierungs-Manager**.
2. Mit der rechten Maustaste des Lizenzservers, und klicken Sie dann auf **Server aktivieren**.
3. Klicken Sie auf **Weiter** auf der Seite Willkommen.
4. Wählen Sie für die Verbindungsmethode **automatische Verbindung (empfohlen)**, und klicken Sie dann auf **Weiter**.
5. Geben Sie die Informationen für Ihr Unternehmen (Ihr Name, Name des Unternehmens, Ihre geografische Region), und klicken Sie dann auf **Weiter**.
6. Geben Sie optional die andere Unternehmensinformationen (z. B. e-Mail- und Unternehmensdateien Adressen), und klicken Sie dann auf **Weiter**. 
7. Stellen Sie sicher, dass **starten Lizenzinstallations-Assistenten jetzt** nicht ausgewählt ist (Wir installieren die Lizenzen in einem späteren Schritt), und klicken Sie dann auf **Weiter**.

Der Lizenzserver ist jetzt damit beginnen, ausstellen und Verwalten von Lizenzen. 