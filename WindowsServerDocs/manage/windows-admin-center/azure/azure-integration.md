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
ms.openlocfilehash: d8758342752ac71c5b700682d4c0f4317dc4cb4e
ms.sourcegitcommit: e817a130c2ed9caaddd1def1b2edac0c798a6aa2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/09/2019
ms.locfileid: "74945221"
---
# <a name="configuring-azure-integration"></a>Konfigurieren der Azure-Integration

>Gilt für: Windows Admin Center, Windows Admin Center Vorschau

Das Windows Admin Center unterstützt mehrere optionale Features, die in Azure-Dienste integriert werden. [Erfahren Sie mehr über die Azure-Integrationsoptionen, die im Windows Admin Center verfügbar sind.](../plan/azure-integration-options.md)

Damit das Windows Admin Center-Gateway mit Azure kommunizieren kann, um Azure Active Directory Authentifizierung für den Gatewayzugriff zu nutzen oder um Azure-Ressourcen in Ihrem Namen zu erstellen (z. b. zum schützen virtueller Computer, die im Windows Admin Center mithilfe der Azure-Website verwaltet werden Wiederherstellung), müssen Sie zunächst Ihr Windows Admin Center-Gateway bei Azure registrieren. Sie müssen dies nur einmal für Ihr Windows Admin Center-Gateway durchführen. diese Einstellung wird beibehalten, wenn Sie Ihr Gateway auf eine neuere Version aktualisieren.

## <a name="register-your-gateway-with-azure"></a>Registrieren Ihres Gateways bei Azure

Wenn Sie zum ersten Mal versuchen, ein Azure-Integrations Feature in Windows Admin Center zu verwenden, werden Sie aufgefordert, das Gateway in Azure zu registrieren. Sie können das Gateway auch registrieren, indem Sie die Registerkarte **Azure** in den Einstellungen des Windows Admin Centers aufrufen. Beachten Sie, dass nur Windows Admin Center-gatewayadministratoren das Windows Admin Center-Gateway bei Azure registrieren können. [Erfahren Sie mehr über Benutzer-und Administrator Berechtigungen in Windows Admin Center](../configure/user-access-control.md#gateway-access-role-definitions).

Mit den durchgeführten in-Product-Schritten wird eine Azure AD-App in Ihrem Verzeichnis erstellt, die es Windows Admin Center ermöglicht, mit Azure zu kommunizieren. Wechseln Sie zum Anzeigen der automatisch erstellten Azure AD-App auf der Registerkarte **Azure** in den Einstellungen des Windows Admin Centers. Mit der **Ansicht in Azure** können Sie die Azure AD-App im Azure-Portal anzeigen. 

Die erstellte Azure AD-App wird für alle Punkte der Azure-Integration im Windows Admin Center verwendet, einschließlich [Azure AD Authentifizierung beim Gateway](../configure/user-access-control.md#azure-active-directory). Das Windows Admin Center konfiguriert automatisch die erforderlichen Berechtigungen zum Erstellen und Verwalten von Azure-Ressourcen in Ihrem Namen:

- Azure Active Directory Graph
    - Directory.AccessAsUser.All
    - User.Read
- Azure-Dienstverwaltung
    - user_impersonation

### <a name="manual-azure-ad-app-configuration"></a>Manuelle Azure AD-App-Konfiguration

Wenn Sie eine Azure AD-App manuell konfigurieren möchten, anstatt die Azure AD-App zu verwenden, die während der gatewayregistrierung automatisch von Windows Admin Center erstellt wird, müssen Sie die folgenden Schritte ausführen.

1. Erteilen Sie der Azure AD App die erforderlichen API-Berechtigungen, die oben aufgeführt sind. Navigieren Sie hierzu zu ihrer Azure AD-App im Azure-Portal. Wechseln Sie zum Azure-Portal > **Azure Active Directory** > **App-Registrierungen** > Wählen Sie Ihre Azure AD-App aus, die Sie verwenden möchten. Klicken Sie dann auf die Registerkarte **API-Berechtigungen** , und fügen Sie die oben aufgeführten API-Berechtigungen hinzu.
2. Fügen Sie die Windows Admin Center-Gateway-URL zu den Antwort-URLs (auch als Umleitungs-URIs bezeichnet) hinzu. Navigieren Sie zu ihrer Azure AD-App, und wechseln Sie dann zu **Manifest**. Suchen Sie den Schlüssel "replyurlswithtype" im Manifest. Fügen Sie innerhalb des Schlüssels ein Objekt hinzu, das zwei Schlüssel enthält: "URL" und "Type". Der Schlüssel "URL" muss über einen Wert der Windows Admin Center-Gateway-URL verfügen, und am Ende wird ein Platzhalter angehängt. Der Schlüssel "Type"-Schlüssel sollte den Wert "Web" aufweisen. Zum Beispiel:

    ```json
    "replyUrlsWithType": [
            {
                    "url": "http://localhost:6516/*",
                    "type": "Web"
            }
    ],
    ```
