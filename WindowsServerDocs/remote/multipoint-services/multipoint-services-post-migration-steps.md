---
title: Multipoint Services-Aufgaben nach der Migration
description: Erfahren Sie, wie Sie die Migration zu Multipoint Services validieren und schließen.
ms.date: 07/29/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 1497cae0-071e-467d-89b8-a7050815d7de
author: lizap
manager: dongill
ms.openlocfilehash: a1d304e95037ad67a8d4f02e1dc17ec3e0485ed8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858893"
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

