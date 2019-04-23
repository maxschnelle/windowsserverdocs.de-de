---
title: MultiPoint Services - Aufgaben nach der Migration
description: Erfahren Sie, wie Sie überprüfen, und schließen Sie die Migration mit MultiPoint Services
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1497cae0-071e-467d-89b8-a7050815d7de
author: lizap
manager: dongill
ms.openlocfilehash: e3fa3c812355a14289ea4eeff3ab1e7e92e00d97
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863501"
---
# <a name="multipoint-services---post-migration-tasks"></a>MultiPoint Services - Aufgaben nach der Migration

>Gilt für: Windows Server 2016

Nach der Migration mit MultiPoint Services in Windows Server 2016 verwenden Sie die folgende Informationen, die Migration zu überprüfen und bereinigen Sie Schritte ausführen.

## <a name="validate-the-migration-by-running-a-pilot-program"></a>Überprüfen Sie die Migration durch Ausführen eines Pilotprogramms

Sie können Ihre MultiPoint Services-Migration überprüfen, indem Sie ein Pilotprojekt in der produktionsumgebung erstellen. Führen Sie auf den Servern das Pilotprojekt, bevor Sie die migrierten Rollendienste in der produktionsumgebung nehmen, um sicherzustellen, dass die Bereitstellung wie erwartet funktioniert. Sollten Sie die Anzahl der Verbindungen auf den ersten langsam erhöhen der Anzahl von Benutzern beim Zugriff auf MultiPoint Server begrenzen.

> [!NOTE] 
> Verwenden Sie immer Testkonten, um die Migration zu testen. Verwenden Sie ein Konto mit Administratorrechten und ein Konto eines gültigen Benutzers ein.

## <a name="retire-the-source-server"></a>Zurückziehen des Quellservers
Nach der Überprüfung der Migrations können Sie Herunterfahren oder trennen Sie den Quellserver aus Ihrem Netzwerk. Wenn der Server konnte die Domäne, entfernen Sie es aus der Domäne, bevor Sie die Verbindung trennen.

