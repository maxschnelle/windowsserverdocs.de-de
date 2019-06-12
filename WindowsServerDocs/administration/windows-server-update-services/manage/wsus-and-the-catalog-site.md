---
title: WSUS und die Katalogwebsite
description: Windows Server Update Service (WSUS)-Thema – Updates in WSUS zu importieren, durch den Zugriff auf die Microsoft Update-Katalog-Website
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f19a8659-5a96-4fdd-a052-29e4547fe51a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 298df36b856cba97ec19126f77456785e5eb6f50
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810930"
---
# <a name="wsus-and-the-catalog-site"></a>WSUS und die Katalogwebsite

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Der Anwendungskatalog-Website ist der Speicherort für Microsoft aus dem Sie Hotfixes und die Hardwaretreiber importieren können.

## <a name="the-microsoft-update-catalog-site"></a>Die Microsoft Update-Katalog-Website
Um Hotfixes in WSUS importieren zu können, müssen Sie die Microsoft Update-Katalog-Website von einem WSUS-Computer zugreifen. Alle Computer, die über die WSUS-Verwaltungskonsole installiert ist, verfügt, und zwar unabhängig davon, ob es sich um einen WSUS-Server ist kann verwendet werden, um Hotfixes aus dem Anwendungskatalog-Website zu importieren. Sie müssen auf dem Computer als Administrator, um die Hotfixes importieren angemeldet werden.

#### <a name="to-access-the-microsoft-update-catalog-site"></a>Zugriff auf die Microsoft Update-Katalog-Website

1.  In der WSUS-Verwaltungskonsole, wählen Sie den obersten Serverknoten oder **Updates**, und klicken Sie in der **Aktionen** auf **Importieren von Updates**. Ein Browserfenster wird auf der Microsoft Update-Katalog-Website geöffnet.

2.  Um die Updates an diesem Standort zugreifen zu können, müssen Sie das ActiveX-Steuerelement von Microsoft Update-Katalog installieren.

3.  Sie können diese Website für Windows-Hotfixes und die Hardwaretreiber durchsuchen. Wenn Sie den gefunden haben, die Sie möchten, fügen sie Ihrem Warenkorb hinzu.

4.  Wenn Sie das Durchsuchen von abgeschlossen haben, wechseln Sie zu dem Warenkorb, und klicken Sie auf den Import Ihrer Updates. Deaktivieren Sie zum Herunterladen der Updates, ohne sie zu importieren, die **direkt in Windows Server Update Services importieren** Kontrollkästchen.

Genehmigte Updates, die von der Microsoft Update-Katalog importiert werden das nächste Mal heruntergeladen, die, das der WSUS-Server synchronisiert wird. Sie werden nicht zum Zeitpunkt des Imports von der Microsoft Update-Katalog-Website heruntergeladen werden.

Beachten Sie, dass Sie die Microsoft Update-Katalog-Website jedoch zugreifen müssen die WSUS-Verwaltungskonsole, um sicherzustellen, dass die Updates im WSUS-kompatiblen Format importiert werden. Wenn Sie manuell die Microsoft Update-Katalog-Website zugreifen, alle Updates, die Sie herunterladen können nicht in der WSUS-Server importiert, aber stattdessen als einzelne heruntergeladen werden *. MSU-Dateien. WSUS verfügt derzeit nicht über einen unterstützten Mechanismus zum Importieren von Dateien in die \*. MSU-Format.

Wenn Sie das Server-Bereinigung Assistenten ausführen, können Updates von Microsoft Update-Katalog importiert, die als nicht genehmigt oder abgelehnt festgelegt werden vom WSUS-Server entfernt. Wenn sie entfernt werden, können sie erneut aus dem Microsoft Update-Katalog importiert werden.

> [!NOTE]
> Sie können Updates, die von Microsoft Update-Katalog importiert werden entfernen, die als nicht genehmigt oder abgelehnt, mit dem WSUS-Server-Cleanup-Assistenten festgelegt werden. Sie können die neu importierten Updates, die zuvor von den WSUS-Systemen über Microsoft Update-Katalog entfernt wurden.

## <a name="restricting-access-to-hotfixes"></a>Einschränken des Zugriffs auf die hotfixes
WSUS-Administratoren sollten Einschränken des Zugriffs auf die Hotfixes, die sie von der Microsoft Update-Katalog-Website heruntergeladen haben. Um diese Einschränkung, die die folgenden Schritte ausführen zu machen:

#### <a name="to-restrict-access-to-hotfixes"></a>Um den Zugriff auf Hotfixes zu beschränken.

1.  Aktivieren Sie Windows-Authentifizierung auf dem IIS-Inhalt Vroot.

    -   Starten Sie IIS-Manager.

    -   Navigieren Sie zu der Inhaltsknoten unter WSUS-Verwaltungswebsite.

    -   Auf der **Inhalt Home** Doppelklicken Sie im Bereich der **Authentifizierung** Option.

    -   Wählen Sie **anonyme Authentifizierung** , und klicken Sie auf **deaktivieren** in die **Aktionen** im rechten Bereich.

    -   Wählen Sie **Windows-Authentifizierung** , und klicken Sie auf **aktivieren** in die **Aktionen** im rechten Bereich.

2.  Erstellen Sie eine WSUS-Zielgruppe für die Computer, die den Hotfix benötigen, und fügen sie der Gruppe hinzu. Weitere Informationen über Computer und Gruppen finden Sie unter [WSUS-Verwaltung von Clientcomputern und WSUS-Computergruppen](managing-wsus-client-computers-and-wsus-computer-groups.md) in diesem Handbuch und Abschnitt [3.3. Konfigurieren von WSUS-Computergruppen](../deploy/2-configure-wsus.md#23-configure-wsus-computer-groups) von Schritt 3: Konfigurieren Sie WSUS, in der WSUS-Bereitstellungshandbuch.

3.  Laden Sie die Dateien für den Hotfix herunter.

4.  Legen Sie die Berechtigungen dieser Dateien, sodass nur Computerkonten dieser Computer gelesen werden können. Sie müssen auch die NETZWERKDIENST-Konto Vollzugriff auf die Dateien zu ermöglichen.

5.  Genehmigen Sie den Hotfix für die WSUS-Zielgruppe, die in Schritt2 erstellt haben.

## <a name="importing-updates-in-different-languages"></a>Importieren von Updates in verschiedenen Sprachen
Die Microsoft Update-Katalog-Website enthält Updates, die mehrere Sprachen zu unterstützen. Es ist sehr **wichtig** entsprechend der sprachunterstützung, die vom WSUS-Server mit den Sprachen, die von diesen Updates unterstützt werden. Wenn der WSUS-Server alle Sprachen, die im Update enthalten nicht unterstützt, wird das Update nicht auf den Clientcomputern bereitgestellt werden. Ebenso wird, wenn ein Update, Unterstützung mehrerer Sprachen auf dem WSUS-Server heruntergeladen, aber noch nicht auf Clientcomputern bereitgestellt wurde, und ein Administrator hebt die Auswahl einer der Sprachen enthalten das Update, das Update wird nicht an die Clients bereitgestellt werden.
