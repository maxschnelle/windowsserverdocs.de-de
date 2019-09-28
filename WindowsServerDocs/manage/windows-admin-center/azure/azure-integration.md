---
title: Konfigurieren der Azure-Integration
description: Konfigurieren der Azure-Integration Windows Admin Center (Project Honolulu). Verbinden Ihres Windows Admin Center-Gateways mit Azure.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 448a8fb3e4340752b673b06f86d5d49211b6b147
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357360"
---
# <a name="configuring-azure-integration"></a>Konfigurieren der Azure-Integration

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Das Windows Admin Center unterstützt mehrere optionale Features, die in Azure-Dienste integriert werden. [Erfahren Sie mehr über die Azure-Integrationsoptionen, die im Windows Admin Center verfügbar sind.](../plan/azure-integration-options.md)

Damit das Windows Admin Center-Gateway mit Azure kommunizieren kann, um Azure Active Directory Authentifizierung für den Gatewayzugriff zu nutzen oder um Azure-Ressourcen in Ihrem Namen zu erstellen (z. b. zum schützen virtueller Computer, die im Windows Admin Center mithilfe der Azure-Website verwaltet werden Wiederherstellung), müssen Sie zunächst Ihr Windows Admin Center-Gateway bei Azure registrieren. Sie müssen dies nur einmal für Ihr Windows Admin Center-Gateway durchführen. diese Einstellung wird beibehalten, wenn Sie Ihr Gateway auf eine neuere Version aktualisieren.

## <a name="register-your-gateway-with-azure"></a>Registrieren Ihres Gateways bei Azure

Wenn Sie zum ersten Mal versuchen, ein Azure-Integrations Feature in Windows Admin Center zu verwenden, werden Sie aufgefordert, das Gateway in Azure zu registrieren. Sie können das Gateway auch registrieren, indem Sie die Registerkarte **Azure** in den Einstellungen des Windows Admin Centers aufrufen.

Mit den durchgeführten in-Product-Schritten wird eine Azure AD-App in Ihrem Verzeichnis erstellt, die es Windows Admin Center ermöglicht, mit Azure zu kommunizieren. Wechseln Sie zum Anzeigen der automatisch erstellten Azure AD-App auf der Registerkarte **Azure** in den Einstellungen des Windows Admin Centers. Mit der **Ansicht in Azure** können Sie die Azure AD-App im Azure-Portal anzeigen. 

Die erstellte Azure AD-App wird für alle Punkte der Azure-Integration im Windows Admin Center verwendet, einschließlich [Azure AD Authentifizierung beim Gateway](../configure/user-access-control.md#azure-active-directory).