---
title: Nahtloses Bereitstellen von RDS mit ARM und Azure Marketplace
description: Erfahren Sie, wie Sie eine kleine RDS-Bereitstellung in Azure erstellen, indem Sie ARM-Vorlagen und den Azure Marketplace verwenden.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f72ceb6-6f90-48f6-bfc3-bdad63984ce7
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 02/10/2017
ms.openlocfilehash: 218e61e5ebe110502ebe139b27607bfeff104fde
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "63712626"
---
# <a name="seamlessly-deploy-rds-with-arm-and-azure-marketplace"></a>Nahtloses Bereitstellen von RDS mit ARM und Azure Marketplace

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Remotedesktopdienste (RDS) sind die Plattform der Wahl, um Windows-Desktops und -Anwendungen kostengünstig zu hosten. Sie können ein [Azure Marketplace-Angebot](#basic-rds-through-the-azure-marketplace) oder eine [Schnellstartvorlage](#customized-rds-using-quickstart-templates) verwenden, um schnell ein RDS für eine Azure IaaS-Bereitstellung zu erstellen. Azure Marketplace erstellt für Sie eine Testdomäne, wodurch es zu einem einfachen und unkomplizierten Mechanismus für Tests und Machbarkeitsstudien wird. Die Schnellstartvorlagen hingegen ermöglichen es Ihnen, eine bestehende Domäne zu verwenden, was sie zu einem hervorragenden Tool für den Aufbau einer Produktionsumgebung machen. Nach der Einrichtung können Sie sich mit den Microsoft-Remotedesktopanwendungen für Windows, Mac, iOS und Android mit den veröffentlichten Desktops und Anwendungen von verschiedenen Plattformen und Geräten verbinden.

## <a name="basic-rds-through-the-azure-marketplace"></a>Grundlegendes RDS über den Azure Marketplace

Die Erstellung Ihrer Bereitstellung über den Azure Marketplace ist der schnellste Weg, um mit der Arbeit zu beginnen. Wenn alles abgeschlossen ist, wird Ihre Umgebung wie die [grundlegende RDS-Architektur](desktop-hosting-logical-architecture.md#basic-deployment) aussehen. Das Angebot erstellt alle erforderlichen RDS-Komponenten – Sie müssen lediglich einige Informationen bereitstellen. 

Die folgenden Informationen müssen Sie bei der Bereitstellung des Marketplace-Angebots angeben:
- Benutzername des Administrators und zugehöriges Kennwort. Dies ist ein neuer Benutzer, der die Bereitstellung verwaltet.
- DNS-Name und AD-Domänenname. Dies sind NEUE Ressourcen, die erstellt werden. Achten Sie darauf, dass die Namen aussagekräftig sind.
- Größe des virtuellen Computers. Sie können die Größe der virtuellen Computer auswählen, die für die RDSH-Endpunkte verwendet werden sollen. Sie können die Größen auch nach der ersten Bereitstellung manuell ändern, um die virtuellen Computer für Ihre Workloads und Kosten zu optimieren.

Führen Sie diese Schritte aus, um Ihre RDS-Bereitstellung mit geringem Speicherbedarf im Azure Marketplace zu erstellen: 

1. Starten Sie die Azure Marketplace-RDS-Bereitstellung:
   1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) an.
   2. Klicken Sie auf **Neu**, um Ihre Bereitstellung hinzuzufügen.
   3. Geben Sie „RDS“ in das Suchfeld ein, und drücken Sie die EINGABETASTE.
   4. Klicken Sie auf **Remotedesktopdienste (RDS) – Einfach – Dev/Test**, und klicken Sie dann auf **Erstellen**.
   5. Befolgen Sie die Schritte im Portal, um RDS zu erstellen und bereitzustellen. Sie werden wichtige Konfigurationsdetails hinzufügen, wie die oben aufgeführten Informationen. 
2. Stellen Sie eine Verbindung mit Ihrer Bereitstellung her. Wenn die Bereitstellung abgeschlossen ist, überprüfen Sie den Abschnitt „Ausgaben“ hinsichtlich der letzten Schritte, um die Bereitstellung abzuschließen und eine Verbindung mit Ihrer Bereitstellung herzustellen.
   1. Laden Sie [dieses PowerShell-Skript](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328) herunter, und führen Sie es auf Ihrem Testgerät aus, um alle Zertifikate zu installieren, die für die Verbindung mit der RDS-Bereitstellung erforderlich sind. 
   
      Dieser Schritt ist nur während der Testphase erforderlich. Wenn Sie RDS in Azure in der Produktionsumgebung bereitstellen, achten Sie darauf, dass Sie bewährte Methoden wie den Erwerb und die Verwendung eines öffentlich vertrauenswürdigen SSL-Zertifikats auf Ihren Webservern beachten.

   2. Wenn Sie dazu aufgefordert werden, melden Sie sich bei Ihrem Azure-Konto an. Wählen Sie das Azure-Abonnement, die Ressourcengruppe und die öffentliche IP-Adresse aus, die für diese neue Bereitstellung erstellt wurden.
   3. Wenn das Skript fertig ist, wird die RD-Webseite in Ihrem Standardbrowser gestartet. Sie können die RD-Webseite erneut überprüfen, indem Sie die URL für die Seite mit der DNS-Adresse vergleichen, die Sie bei der Bereitstellung angegeben haben. 
   
      Melden Sie sich mit den Administratoranmeldeinformationen an, die Sie während der Bereitstellung erstellt haben, um den für Sie veröffentlichten Standarddesktop anzuzeigen. Sie können Benutzern auch die RD-Website senden, um ihre Desktops und Anwendungen zu testen.

      > [!TIP]
      > Haben Sie den Domänennamen oder den Administratorbenutzer vergessen? Sie können zur neuen Ressourcengruppe im Portal zurückkehren, auf **Bereitstellungen** klicken und dann die von Ihnen eingegebenen Parameter anzeigen.

Nachdem Sie jetzt über eine RDS-Bereitstellung verfügen, können Sie [Benutzer hinzufügen und verwalten](rds-user-management.md).

## <a name="customized-rds-using-quickstart-templates"></a>Benutzerdefiniertes RDS mit Schnellstartvorlagen

Sie können Azure Resource Manager-Vorlagen verwenden, um RDS in Azure bereitzustellen. Dies ist besonders hilfreich, wenn Sie eine einfache RDS-Bereitstellung wünschen, aber über vorhandene Komponenten (wie AD) verfügen, die Sie verwenden möchten. Im Gegensatz zum Marketplace-Angebot können Sie weitere Anpassungen vornehmen, z. B. die Verwendung eines vorhandenen AD in einem virtuellen Netzwerk, die Verwendung benutzerdefinierter Betriebssystemimages für die RDSH-VMs und die Überlagerung bei Hochverfügbarkeit für RDS-Komponenten. Nachdem Sie jeder Komponente die Hochverfügbarkeit hinzugefügt haben, wird Ihre Umgebung wie die [hochverfügbare RDS-Architektur](desktop-hosting-logical-architecture.md#highly-available-deployment) aussehen.

Verwenden Sie diese Schritte, um Ihre RDS-Bereitstellung mit geringem Speicherbedarf mit einer Azure RDS-Vorlage zu erstellen: 

1. Wählen Sie Ihre Azure-Schnellstartvorlage aus:
   1. Wechseln Sie zur Website [RDS Azure-Schnellstartvorlagen](https://aka.ms/rdautomation).
   2. Wählen Sie die Vorlage aus, die Ihren Anforderungen entspricht. Stellen Sie sicher, dass Sie alle Voraussetzungen für diese bestimmte Vorlage erfüllen. (Wenn Sie z. B. ein benutzerdefiniertes Image für Ihre virtuellen Computer verwenden möchten, stellen Sie sicher, dass Sie dieses Image bereits in ein Azure-Speicherkonto hochgeladen haben.)
   3. Klicken Sie auf **In Azure bereitstellen**.
   4. Sie müssen einige Details (wie Administratorbenutzername, AD-Domänenname) im Azure-Portal angeben. Dies hängt von der gewählten Vorlage ab.
   5. Klicken Sie auf **Kaufen**.
2. Stellen Sie eine Verbindung mit Ihrer Bereitstellung her. 
   1. Laden Sie [dieses PowerShell-Skript](https://gallery.technet.microsoft.com/Azure-Resource-Manager-4ea7e328) herunter, und führen Sie es auf Ihrem Testgerät aus, um alle Zertifikate zu installieren, die für die Verbindung mit der RDS-Bereitstellung erforderlich sind. 
   
      Dieser Schritt ist nur während der Testphase erforderlich. Wenn Sie RDS in Azure in der Produktionsumgebung bereitstellen, achten Sie darauf, dass Sie bewährte Methoden wie den Erwerb und die Verwendung eines öffentlich vertrauenswürdigen SSL-Zertifikats auf Ihren Webservern beachten.

   2. Wenn Sie dazu aufgefordert werden, melden Sie sich bei Ihrem Azure-Konto an. Wählen Sie das Azure-Abonnement, die Ressourcengruppe und die öffentliche IP-Adresse aus, die für diese neue Bereitstellung erstellt wurden.
   3. Wenn das Skript fertig ist, wird die RD-Webseite in Ihrem Standardbrowser gestartet. Sie können die RD-Webseite erneut überprüfen, indem Sie die URL für die Seite mit der DNS-Adresse vergleichen, die Sie bei der Bereitstellung angegeben haben. 
   
      Melden Sie sich mit den Administratoranmeldeinformationen an, die Sie während der Bereitstellung erstellt haben, um den für Sie veröffentlichten Standarddesktop anzuzeigen. Sie können Benutzern auch die RD-Website senden, um ihre Desktops und Anwendungen zu testen.

      > [!TIP]
      > Haben Sie den Domänennamen oder den Administratorbenutzer vergessen? Sie können zur neuen Ressourcengruppe im Portal zurückkehren, auf **Bereitstellungen** klicken und dann die von Ihnen eingegebenen Parameter anzeigen.

Nachdem Sie jetzt über eine RDS-Bereitstellung verfügen, können Sie [Benutzer hinzufügen und verwalten](rds-user-management.md).
