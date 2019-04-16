---
title: Konfigurieren der Azure-Integration
description: Konfigurieren der Azure-Integration Windows Admin Center (Projekt Honolulu). Verbinden das Windows Admin Center-Gateway mit Azure.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 09/19/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 38b973680463cdebc1b3168e447abfcf1caba6b5
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296917"
---
# Konfigurieren der Azure-integration

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Windows Admin Center unterstützt verschiedene optionale Features, die mit Azure-Diensten integrieren lassen. [Informationen Sie zu den Integrationsoptionen von Azure mit Windows Admin Center verfügbar.](../plan/azure-integration-options.md)

Um das Windows Admin Center-Gateway für die Kommunikation mit Azure, Azure Active Directory-Authentifizierung für den Gateway-Zugriff zu nutzen oder das Erstellen von Azure-Ressourcen in Ihrem Auftrag (z. B. zum Schutz von VMs in Windows Admin Center verwaltet mithilfe von Azure Site zu ermöglichen. Wiederherstellung), müssen Sie zunächst das Windows Admin Center-Gateway mit Azure registrieren. Sie müssen nur dazu, nachdem die Einstellung für Ihr Windows Admin Center-Gateway - beibehalten wird, wenn Sie das Gateway auf eine neuere Version aktualisieren.

## Registrieren Sie Ihr Gateway mit Azure

Beim ersten Sie versuchen, ein Feature von Azure-Integration in Windows Admin Center verwenden, werden Sie aufgefordert, das Gateway zu registrieren. Sie können auch das Gateway registrieren, indem Sie auf der Registerkarte " **Azure** " unter "Einstellungen" Windows Admin Center.

Die schrittweise Anleitung in die Produkte Schritte werden eine Azure AD-app in Ihrem Verzeichnis erstellt, die Windows Admin Center für die Kommunikation mit Azure ermöglicht. Um die Azure AD-app anzeigen, die automatisch erstellt wird, wechseln Sie auf der Registerkarte " **Azure** " Windows Admin Center-Einstellungen. Die **Ansicht in Azure** -Link können Sie die Azure AD-app im Azure-Portal anzeigen. 

Die Azure AD-app erstellt wird für alle Punkte der Azure-Integration in Windows Admin Center, einschließlich [Azure AD-Authentifizierung, um das Gateway](../configure/user-access-control.md#azure-active-directory)verwendet.