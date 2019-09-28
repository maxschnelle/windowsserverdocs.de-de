---
title: Multipoint Services-Aufgaben nach der Migration
description: Erfahren Sie, wie Sie die Migration zu Multipoint Services validieren und schließen.
ms.custom: na
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1497cae0-071e-467d-89b8-a7050815d7de
author: lizap
manager: dongill
ms.openlocfilehash: 3102a442b4668856050f603f30f57f6bbed20654
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389019"
---
# <a name="multipoint-services---post-migration-tasks"></a>Multipoint Services-Aufgaben nach der Migration

>Gilt für: Windows Server 2016

Nachdem Sie zu Multipoint Services in Windows Server 2016 migriert haben, verwenden Sie die folgenden Informationen, um die Migration zu überprüfen und um Bereinigungs Schritte auszuführen.

## <a name="validate-the-migration-by-running-a-pilot-program"></a>Überprüfen der Migration durch Ausführen eines Pilotprogramms

Sie können Ihre Multipoint Services-Migration überprüfen, indem Sie in der Produktionsumgebung ein Pilotprojekt erstellen. Führen Sie das Pilotprojekt auf den Servern aus, bevor Sie die migrierten Rollen Dienste in der Produktionsumgebung ablegen, um sicherzustellen, dass die Bereitstellung erwartungsgemäß funktioniert. Beschränken Sie die Anzahl der Verbindungen zunächst, und erhöhen Sie die Anzahl der Benutzer, die auf Multipoint Services zugreifen.

> [!NOTE] 
> Verwenden Sie immer Testkonten, um die Migration zu testen. Verwenden Sie ein Konto mit Administratorrechten und einem Konto für einen gültigen Benutzer.

## <a name="retire-the-source-server"></a>Zurückziehen des Quellservers
Nachdem Sie die Migration überprüft haben, können Sie den Quell Server von Ihrem Netzwerk Herunterfahren oder trennen. Wenn der Server einer Domäne beigetreten ist, entfernen Sie ihn aus der Domäne, bevor Sie die Verbindung trennen.

