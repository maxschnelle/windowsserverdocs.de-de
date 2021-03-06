---
title: Verwalten von SharePoint Online in Windows Server Essentials
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 282f3634-6de6-4691-803c-df6c3c16660d
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 66e5a2c8781e5c9602ba667e15ac789732767be3
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89626090"
---
# <a name="manage-sharepoint-online-in-windows-server-essentials"></a>Verwalten von SharePoint Online in Windows Server Essentials

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können Ihre SharePoint Online-Bibliotheken und-Team Websites über das Dashboard verwalten, ohne sich bei Microsoft 365 anzumelden, wenn Sie Microsoft 365 in Ihren Windows Server Essentials-Server integrieren. Sie erhalten SharePoint Online-Bibliotheken und-Team Websites mit jedem Microsoft 365 Geschäftsplan. [Erfahren Sie, wie Sie Microsoft 365 in Ihren Server integrieren.](Manage-Office-365-in-Windows-Server-Essentials.md)

 Als Bonus können Ihre Benutzer die My Server 2012 R2-App verwenden, um von überall aus mithilfe Ihres mobilen Geräts oder Windows Phone auf Dateien in Ihren SharePoint Online-Bibliotheken zuzugreifen. [Wo erhalte ich die My Server-App?](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)

 Sie haben SharePoint noch nicht getestet? [Aktuelle Möglichkeiten](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/get-started-with-sharepoint-2013-HA102772778.aspx)

## <a name="where-on-the-dashboard-will-i-manage-my-libraries-and-team-sites"></a>Wo auf dem Dashboard verwalte ich meine Bibliotheken und Teamwebsites?
 Sie verwenden die neue Registerkarte **SharePoint Online** , die dem Bereich **Speicher** des Dashboards hinzugefügt wird, wenn Sie Microsoft 365 in den Server integrieren, um SharePoint Online-Ressourcen zu verwalten.


## <a name="what-can-i-manage-from-the-dashboard"></a>Was kann ich über das Dashboard verwalten?

### <a name="manage-your-online-libraries"></a>Verwalten der Onlinebibliotheken

- **Fügen Sie eine Bibliothek hinzu.** Verwenden Sie auf der Registerkarte **SharePoint-Bibliotheken** die Option **Bibliothek hinzufügen**. Sie können weiterhin Ihre üblichen Optionen wählen:
  - Wählen Sie eine Teamwebsite und den Bibliothekstyp.
  - Entscheiden Sie sich, ob Sie die Versionskontrolle verwenden möchten.
  - Weisen Sie Zugriffsberechtigungen zu.
     **Tipp:** Verwenden Sie **Website Berechtigungen anzeigen**, um herauszufinden, welche Team Website-Berechtigungen Ihre Bibliothek erbt, wenn Sie keine Berechtigungen zuweisen.
- **Öffnen Sie eine Bibliothek.** Wenn Sie mit dem Inhalt der Bibliothek arbeiten möchten, müssen Sie ihn in Microsoft 365 öffnen. Wählen Sie die Bibliothek aus, und klicken Sie auf **Bibliothek öffnen**. Welche Möglichkeiten Sie mit dem Inhalt haben, hängt von den Anmelde Informationen ab, mit denen Sie sich bei SharePoint Online anmelden.
- **Ändern Sie die Versionskontrolle oder Zugriffsberechtigungen.** Verwenden Sie **Eigenschaften der Bibliothek anzeigen**, um die Versionskontrollen oder Zugriffsberechtigungen für die Bibliothek anzuzeigen oder zu ändern.
- **Löschen Sie eine Bibliothek.** Nachdem Sie sichergestellt haben, dass in der Bibliothek nichts mehr gespeichert ist, was Sie später benötigen, wählen Sie die Bibliothek aus, und klicken Sie auf **Bibliothek löschen**. **Warnung:** Bevor Sie eine SharePoint Online-Bibliothek löschen, müssen Sie alle Dateien speichern, die Sie an einem anderen Speicherort aufbewahren möchten. Wenn Sie eine Bibliothek aus SharePoint löschen, wird alles dauerhaft gelöscht. Es gibt keine Möglichkeit, etwas davon wieder abzurufen.

### <a name="manage-your-team-sites"></a>Verwalten der Teamwebsites

- **SharePoint-Team Websites verwalten.** Mithilfe der Aktion **Team Websites verwalten** können Sie sich beim Microsoft 365 und der Verwaltung Ihrer SharePoint Online-Team Websites anmelden. Welche Möglichkeiten Sie in Microsoft 365 haben, wird durch das Onlinekonto bestimmt, mit dem Sie sich anmelden. Wenn Sie Microsoft 365 schließen und zum Dashboard zurückkehren, klicken Sie auf **Aktualisieren** , um die Änderungen anzuzeigen.
- **Anzeigen oder Ändern der Berechtigungen von Team Websites.** Da eine Bibliothek standardmäßig Berechtigungen von der Team Website erbt, ist es hilfreich, einfachen Zugriff auf die Teamwebsite zu haben. Wenn Sie Berechtigungen für eine Team Website anzeigen oder ändern möchten, wählen Sie die Team Website oder eine Ihrer Bibliotheken aus, und klicken Sie auf **Website Berechtigungen anzeigen**. **Tipp:** Benötigen Sie Hilfe bei den fein Punkten der SharePoint Team Site-Berechtigungen? Unter den Teamwebsite-Berechtigungen steht ein nützlicher Link für [Weitere Informationen](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=5&origin=HA102771924) bereit.

## <a name="tips"></a>Tipps

-   **Klicken Sie auf aktualisieren, um die letzten Änderungen anzuzeigen, die im Microsoft 365-Portal vorgenommen wurden.** Sie müssen die Anzeige aktualisieren, nachdem Sie Microsoft 365 geöffnet haben, um SharePoint Online zu verwalten. Wenn Sie das Dashboard länger geöffnet haben, klicken Sie auf **Aktualisieren**, um sicherzustellen, dass Sie die neuen Änderungen sehen.

-   **Welche Aktionen Sie in SharePoint Online ausführen können, hängt davon ab, ob Sie im Dashboard oder in Microsoft 365 arbeiten.** Auf dem Dashboard werden SharePoint Online-Änderungen mit dem Administrator Konto für Microsoft 365 Integration vorgenommen. Wenn Sie sich jedoch über das Dashboard bei Microsoft 365 anmelden, legen die Zugriffsberechtigungen für das Onlinekonto, das Sie verwenden, fest, was Sie tun können.

     Um das Administrator Konto für Microsoft 365 Integration zu ermitteln, öffnen Sie die Registerkarte **Microsoft 365** auf dem Dashboard.

## <a name="other-things-you-might-want-to-do"></a>Andere mögliche Aktionen

-   [Verwenden Sie eine My Server-App, um von überall aus mit den SharePoint Online-Bibliotheken zu arbeiten](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)

-   [Erfahren Sie mehr über das Zuweisen von Berechtigungen für SharePoint-Teamwebsites](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=5&origin=HA102771924)

-   [Finden Sie heraus, was Sie mit den SharePoint-Funktionen machen können](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/get-started-with-sharepoint-2013-HA102772778.aspx)

-   [Sehen Sie sich die Microsoft 365 verfügbaren Geschäftspläne an](https://office.microsoft.com/business/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_what-is-office-365-for_Text)

-   [Integrieren von Microsoft 365 in Ihren Server](Manage-Office-365-in-Windows-Server-Essentials.md)

-   [Verwalten Sie Microsoft-Onlinedienste über das Dashboard](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
