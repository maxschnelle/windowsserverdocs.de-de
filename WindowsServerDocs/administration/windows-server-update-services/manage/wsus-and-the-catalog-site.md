---
title: WSUS und Katalog-Website
description: 'Windows Server Update Service (WSUS)-Thema: Importieren von Hotfixes in WSUS durch Zugriff auf die Microsoft Update-Katalog Website'
ms.topic: article
ms.assetid: f19a8659-5a96-4fdd-a052-29e4547fe51a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 25a9852935c47e0c005d78ae7ea24d14c7c1a546
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896784"
---
# <a name="wsus-and-the-catalog-site"></a>WSUS und Katalog-Website

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Katalog Site ist der Microsoft-Speicherort, von dem Sie Hotfixes und Hardwaretreiber importieren können.

## <a name="the-microsoft-update-catalog-site"></a>Die Microsoft Update Katalog-Website
Um Hotfixes in WSUS zu importieren, müssen Sie von einem WSUS-Computer aus auf den Microsoft Update-Katalog Standort zugreifen. Alle Computer, auf denen die WSUS-Verwaltungskonsole installiert ist, unabhängig davon, ob es sich um einen WSUS-Server handelt, können zum Importieren von Hotfixes vom Katalog Standort verwendet werden. Sie müssen als Administrator auf dem Computer angemeldet sein, um die Hotfixes zu importieren.

#### <a name="to-access-the-microsoft-update-catalog-site"></a>So greifen Sie auf die Microsoft Update Katalog-Website zu

1.  Wählen Sie in der WSUS-Verwaltungskonsole entweder den obersten Server Knoten oder **Updates**aus, und klicken Sie im **Aktions** Bereich auf **Updates importieren**. Ein Browserfenster wird auf der Microsoft Update Katalog-Website geöffnet.

2.  Um auf die Updates an diesem Standort zuzugreifen, müssen Sie das Microsoft Update Catalog-ActiveX-Steuerelement installieren.

3.  Sie können diese Website nach Windows-Hotfixes und Hardware Treibern durchsuchen. Wenn Sie die gewünschten gefunden haben, fügen Sie Sie Ihrem Warenkorb hinzu.

4.  Wenn Sie das Durchsuchen abgeschlossen haben, wechseln Sie zum Warenkorb, und klicken Sie auf Importieren, um Ihre Updates zu importieren. Deaktivieren Sie das Kontrollkästchen **direkt in Windows Server Update Services importieren** , um die Updates herunterzuladen, ohne Sie zu importieren.

Genehmigte Updates, die von der Microsoft Update Katalog-Website importiert werden, werden bei der nächsten Synchronisierung des WSUS-Servers heruntergeladen. Sie werden nicht zum Zeitpunkt des Imports von der Microsoft Update Katalog-Website heruntergeladen.

Beachten Sie, dass Sie über die WSUS-Konsole auf die Microsoft Update Katalog-Website zugreifen müssen, um sicherzustellen, dass die Updates in einem WSUS-kompatiblen Format importiert werden. Wenn Sie manuell auf die Microsoft Update Katalog-Website zugreifen, werden alle Updates, die Sie herunterladen, nicht in den WSUS-Server importiert, sondern als Einzelperson * heruntergeladen. MSU-Dateien. WSUS verfügt zurzeit nicht über einen unterstützten Mechanismus zum Importieren von Dateien in \* . MSU-Format.

Wenn Sie den-Server Bereinigungs-Assistenten ausführen, werden Updates, die aus dem Microsoft Update Katalog importiert wurden und als nicht genehmigt oder abgelehnt festgelegt wurden, möglicherweise vom WSUS-Server entfernt. Wenn Sie entfernt werden, können Sie aus dem Microsoft Update Katalog neu importiert werden.

> [!NOTE]
> Sie können Updates entfernen, die aus dem Microsoft Update Katalog importiert werden, die entweder als nicht genehmigt oder abgelehnt festgelegt wurden, indem Sie den WSUS-Server Bereinigungs-Assistenten ausführen. Sie können Updates, die zuvor aus ihren WSUS-Systemen entfernt wurden, über den Microsoft Update Katalog erneut importieren.

## <a name="restricting-access-to-hotfixes"></a>Einschränken des Zugriffs auf Hotfixes
WSUS-Administratoren können den Zugriff auf die Hotfixes beschränken, die Sie von der Microsoft Update Katalog-Website heruntergeladen haben. Führen Sie die folgenden Schritte aus, um diese Einschränkung vorzunehmen:

#### <a name="to-restrict-access-to-hotfixes"></a>So schränken Sie den Zugriff auf Hotfixes ein

1.  Aktivieren Sie die Windows-Authentifizierung für den IIS-Inhalts-vroot.

    -   Starten Sie den IIS-Manager.

    -   Navigieren Sie unter WSUS-Verwaltungs Website zum Knoten Inhalt.

    -   Doppelklicken Sie im **Inhalts** Startbereich auf die Option **Authentifizierung** .

    -   Wählen Sie **anonyme Authentifizierung** aus, und klicken Sie im **Aktions** Bereich auf der rechten Seite auf **Deaktivieren** .

    -   Wählen Sie **Windows-Authentifizierung** aus, und klicken Sie im **Aktions** Bereich auf der rechten Seite auf **aktivieren** .

2.  Erstellen Sie eine WSUS-Zielgruppe für die Computer, für die der Hotfix erforderlich ist, und fügen Sie Sie der Gruppe hinzu. Weitere Informationen zu Computern und Gruppen finden Sie unter [Verwalten von WSUS-Client Computern und WSUS-Computer Gruppen](managing-wsus-client-computers-and-wsus-computer-groups.md) in diesem Handbuch und Abschnitt [3,3. Konfigurieren Sie WSUS-Computer Gruppen](../deploy/2-configure-wsus.md#23-configure-wsus-computer-groups) von Schritt 3: Konfigurieren von WSUS im WSUS-Bereitstellungs Handbuch.

3.  Laden Sie die Dateien für den Hotfix herunter.

4.  Legen Sie die Berechtigungen für diese Dateien so fest, dass Sie nur von Computer Konten dieser Computer gelesen werden können. Außerdem müssen Sie dem Netzwerkdienst Konto Vollzugriff auf die Dateien gestatten.

5.  Genehmigen Sie den Hotfix für die WSUS-Zielgruppe, die Sie in Schritt 2 erstellt haben.

## <a name="importing-updates-in-different-languages"></a>Importieren von Updates in verschiedenen Sprachen
Die Microsoft Update Catalog-Website enthält Updates, die mehrere Sprachen unterstützen. Es ist sehr **wichtig** , die vom WSUS-Server unterstützten Sprachen mit den von diesen Updates unterstützten Sprachen abzugleichen. Wenn der WSUS-Server nicht alle Sprachen unterstützt, die im Update enthalten sind, wird das Update nicht auf Client Computern bereitgestellt. Ebenso gilt: Wenn ein Update, das mehrere Sprachen unterstützt, auf den WSUS-Server heruntergeladen, aber noch nicht auf Client Computern bereitgestellt wurde und ein Administrator eine der in diesem Update enthaltenen Sprachen deaktiviert, wird das Update nicht auf den Clients bereitgestellt.
