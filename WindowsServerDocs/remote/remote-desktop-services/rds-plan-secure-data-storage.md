---
title: Remotedesktopdienste - sicheren Datenspeicher
description: Planungsinformationen für das sichere Speichern von Daten mithilfe von Benutzerprofil-Datenträgern (UPDs) in RDS.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 37b7f68e-7c3a-4190-a52f-99ae96885fae
author: lizap
ms.author: elizapo
ms.date: 11/21/2016
manager: dongill
ms.openlocfilehash: c3c7be624e3b093347807a5ee131270d3c802f1a
ms.sourcegitcommit: d888e35f71801c1935620f38699dda11db7f7aad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66805160"
---
# <a name="remote-desktop-services---secure-data-storage-with-upds"></a>Remotedesktopdienste - sicheren Datenspeicher mit dem Benutzerprofil-Datenträger

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016

Ressourcen für die Business Store, Personalisierung von Benutzerdaten und Einstellungen sicher lokal oder in Azure. RD-Sitzungshosts AD-Authentifizierung verwenden, und steigern der Benutzerproduktivität mit den benötigten Ressourcen in einer personalisierten Umgebung sicher. 

Sicherstellen, dass Benutzer über eine einheitliche, unabhängig von den Endpunkt, von denen sie Zugriff auf die Remoteressourcen, ist ein wichtiger Aspekt der Verwaltung einer RDS-Bereitstellung, verfügen. Benutzerprofil-Datenträgern (UPDs) können Benutzerdaten, Anpassungen und Anwendungseinstellungen, folgen Sie einen Benutzer in einer einzelnen Sammlung. Ein Benutzerprofil-Datenträger ist ein pro-Benutzer, sammlungsspezifischen VHD-Datei, die in einer zentralen Freigabe, die bereitgestellt wird, um der Sitzung eines Benutzers, bei seiner Anmeldung: dem Benutzerprofil-Datenträger wird als lokales Laufwerk behandelt, für die Dauer der Sitzung, gespeichert. 

Aus Sicht des Benutzers dem Benutzerprofil-Datenträger bietet eine Famililar: sie speichern ihre Dokumente in ihre Dokumente (dazu, was angezeigt wird, werden von einem lokalen Laufwerk), Ordner ändern ihre app-Einstellungen wie gewohnt, und alle Änderungen an ihrer Windows-Umgebung vornehmen. Alle diese Daten, einschließlich der Registrierungsstruktur, auf dem Benutzerprofil-Datenträger gespeichert und bleiben in einer zentralen Netzwerkfreigabe verfügen. Benutzerprofil-Datenträger sind nur für den Benutzer verfügbar, wenn der Benutzer aktiv mit einem Desktop- oder RemoteApp verbunden ist. Benutzerprofil-Datenträger können nur innerhalb einer Auflistung wechseln, da der gesamte benutzerorder `C:\Users\<username\>` Verzeichnis (einschließlich AppData\Local) auf dem Benutzerprofil-Datenträger gespeichert ist.

Sie können [PowerShell-Cmdlets](https://technet.microsoft.com/library/jj215443.aspx) , bestimmen den Pfad zu den zentralen Freigabe, die Größe jeder Benutzerprofil-Datenträger und die Ordner einbezogen oder das Benutzerprofil auf dem Benutzerprofil-Datenträger gespeichert ausgeschlossen werden. Alternativ können Sie Benutzerprofil-Datenträger mithilfe von Server Manager aktivieren, indem Sie zu **Remote Desktop Services** > **Sammlungen** > **Sammlung Desktops**  >  **Desktop Sammlungseigenschaften** > **Benutzerprofil-Datenträger**. Beachten Sie, dass Sie aktivieren oder Deaktivieren von Benutzerprofil-Datenträger für alle Benutzer, der eine ganze Sammlung, nicht für bestimmte Benutzer in dieser Auflistung. Benutzerprofil-Datenträger müssen in einer zentralen Dateifreigabe gespeichert werden, in denen die Server in der Auflistung mit Vollzugriff verfügen. 

Sie erreichen hochverfügbarkeit für Ihre UPDs durch Speichern in Azure mit ["direkte Speicherplätze"](rds-storage-spaces-direct-deployment.md). 