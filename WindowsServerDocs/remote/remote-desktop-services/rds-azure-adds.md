---
title: Azure Active Directory-Domänendienste und Remote Desktop Services
description: Informationen Sie zum Integrieren von Azure Active Directory-Domänendienste in Ihre RDS-Bereitstellung.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 10/02/2017
ms.tgt_pltfrm: na
ms.topic: article
author: christianmontoya
ms.localizationpriority: medium
ms.openlocfilehash: e60cf70f1f91ad87046bedf024fe9afc459075b6
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1614516"
---
# <a name="integrate-azure-ad-domain-services-with-your-rds-deployment"></a>Integrieren von Azure Active Directory-Domänendienste in Ihrer Bereitstellung RDS

Sie können in Ihrer Bereitstellung Remote Desktop Services anstelle einer Windows Server Active Directory [Azure Active Directory-Domänendienste](/azure/active-directory-domain-services/active-directory-ds-overview) (Azure AD DS) verwenden. Azure AD DS können Sie Ihre vorhandenen Azure AD Identitäten, sich mit der klassischen Windows-Arbeitslasten zu verwenden.

Azure AD DS ermöglichen Folgendes: 
- Erstellen einer Azure-Umgebung mit einer lokalen Domäne für geboren in--Cloud-Organisationen. 
- Erstellen einer isolierten Azure-Umgebung mit der gleichen Identitäten für Ihre lokalen und online-Umgebung verwendet werden, ohne eine Standort-zu-Standort-VPN- oder ExpressRoute erstellen. 

Wenn Sie die Integration von Azure AD DS in Ihrer Bereitstellung Remotedesktop abgeschlossen haben, wird Ihre Architektur wie folgt aussehen:

![Ein mit RDS mit Azure AD DS-Architekturdiagramm](media/aadds-rds.png)

Um herauszufinden, wie diese Architektur mit anderen RDS-Bereitstellungsszenarien verglichen, checken Sie [Remote Desktop Services Architekturen](desktop-hosting-logical-architecture.md).

Um ein besseres Verständnis von Azure AD DS erhalten möchten, probieren Sie die [Azure AD DS-Übersicht](/azure/active-directory-domain-services/active-directory-ds-overview) und [wie Sie entscheiden, ob Azure AD DS für Ihre Anwendungsfall die richtige Wahl ist](/azure/active-directory-domain-services/active-directory-ds-comparison).

Verwenden Sie die folgenden Informationen zum Bereitstellen von Azure AD DS mit RDS.

## <a name="prerequisites"></a>Voraussetzungen

Vor dem bringen Sie Ihre Identitäten aus dem Azure Active Directory in eine RDS-Bereitstellung [Konfigurieren Azure AD zum Speichern der Hash Kennwörter für Ihre Benutzer Identitäten](/azure/active-directory-domain-services/active-directory-ds-getting-started-password-sync)verwendet. Geboren in--Cloud-Organisationen müssen keine zusätzlichen Änderungen in ihrem Verzeichnis anzuzeigen. lokalen Organisationen müssen jedoch zulassen Kennworthashes synchronisiert und in Azure AD, die nicht zulässig, einige Organisationen möglicherweise gespeichert werden. Die Benutzer müssen ihre Kennwörter zurücksetzen, nachdem Sie diese konfigurationsänderung vorgenommen haben.

## <a name="deploy-azure-ad-ds-and-rds"></a>Bereitstellen von Azure AD DS und RDS 
Verwenden Sie die folgenden Schritte zum Bereitstellen von Azure AD DS und RDS.

1. [Azure AD DS](/azure/active-directory-domain-services/active-directory-ds-getting-started)zu aktivieren. Beachten Sie, dass der verknüpfte Artikel folgende Aktionen ausführt:
   - Durch das Erstellen der geeigneten Azure AD-Gruppen für die Domänenadministration.
   - Wenn Sie erzwingen, dass Benutzer ihre Kennwörter ändern, sodass ihre Konten mit Azure AD DS arbeiten können möglicherweise zu markieren.
   
2. Einrichten von RDS. Sie können eine Azure Vorlage verwenden oder manuelles Bereitstellen von RDS.
   - Verwenden Sie die [vorhandene AD-Vorlage](https://azure.microsoft.com/resources/templates/rds-deployment-existing-ad/). Stellen Sie sicher, dass Sie Folgendes anpassen:
   
      - **Einstellungen**
         - **Ressourcengruppe**: Verwenden Sie die Ressourcengruppe, in der Sie die RDS-Ressourcen erstellen möchten.
         > [!NOTE] 
         > Bis zu diesem Zeitpunkt dies die gleiche Ressourcengruppe werden vorhanden ist, in dem das virtuelle Netzwerk aus Azure Ressourcen-Manager hat.

         - **DNS-Bezeichnung Präfix**: Geben Sie die URL, die Benutzer Zugriff auf RD-Website verwenden sollen.
         - **Ad Domain Name**: Geben Sie den vollständigen Namen der Azure AD-Instanz, zum Beispiel "contoso.onmicrosoft.com" oder "contoso.com".
         - **Ad Vnet Name** und **Ad Subnetz Name**: Geben Sie die gleichen Werte, die Sie bei der Erstellung des Azure-Ressourcen-Manager virtuelles Netzwerks verwendet. Dies ist das Subnetz, mit dem die RDS-Ressourcen verbinden möchten.
         - **Und **-Kennwort Admin**** : Geben Sie die Anmeldeinformationen für einen Administrator, der Mitglied der Gruppe der **Administratoren für AAD DC** in Azure Active Directory ist.
   
      - **Vorlage**
         - Entfernen Sie alle Eigenschaften des **DnsServers**: nach der Auswahl der **Vorlage bearbeiten** aus der Seite "Azure Schnellstart Vorlage", "DnsServers" Suchen und entfernen Sie die Eigenschaft. 

            Beispielsweise vor dem Entfernen der **DnsServers** -Eigenschaft:
      
            ![Azure Schnellstart-Vorlage mit DnsSettings-Eigenschaft](media/rds-remove-dnssettings-before.png)

            Und hier dieselbe Datei nach dem Entfernen der-Eigenschaft ist:

            ![Azure Schnellstart-Vorlage mit entfernt DnsSettings-Eigenschaft](media/rds-remove-dnssettings-after.png)
   
   - [RDS bereitstellen manuell](rds-deploy-infrastructure.md). 

