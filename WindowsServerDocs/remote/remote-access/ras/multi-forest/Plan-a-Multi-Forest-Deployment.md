---
title: Planen einer Bereitstellung mit mehreren Gesamtstrukturen
description: Dieses Thema ist Teil des Leitfadens Bereitstellen des Remotezugriffs in einer Umgebung mit mehreren Gesamtstrukturen in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8acc260f-d6d1-4d32-9e3a-1fd0b2a71586
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a2f14fdb2fd3ab6f0a89c8d8c1a8853041dcba94
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281010"
---
# <a name="plan-a-multi-forest-deployment"></a>Planen einer Bereitstellung mit mehreren Gesamtstrukturen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema werden die zum Konfigurieren des Remotezugriffs für eine Bereitstellung mit mehreren Gesamtstrukturen erforderlichen Planungsschritte beschrieben.  
  
## <a name="prerequisites"></a>Vorraussetzungen  
Bevor Sie mit der Bereitstellung dieses Szenarios beginnen, sollten Sie die Liste der wichtigen Anforderungen lesen:  
  
-   Eine bidirektionale Vertrauensstellung ist erforderlich.  
  
## <a name="plan-trust-between-forests"></a>Planen von Vertrauensstellungen zwischen Gesamtstrukturen  
Wenn Sie den Zugriff auf Ressourcen von einer neuen Gesamtstruktur ermöglichen, für Clients aus der neuen Gesamtstruktur die Verwendung von DirectAccess zulassen oder RAS-Server in der neuen Gesamtstruktur als Einstiegspunkte für die Remotezugriffsbereitstellung hinzufügen möchten, muss eine volle Vertrauenswürdigkeit, d. h. eine bidirektionale transitive Vertrauensstellung, zwischen den beiden Gesamtstrukturen konfiguriert werden. Informationen hierzu finden Sie unter [Vertrauenstypen](https://technet.microsoft.com/library/cc775736.aspx). Die volle Vertrauenswürdigkeit zwischen Gesamtstrukturen ist die Voraussetzung dafür, dass in einer Bereitstellung mit mehreren Gesamtstrukturen Administratoren bestimmte Vorgänge ausführen können. Zu diesen Vorgängen gehören das Bearbeiten von Gruppenrichtlinienobjekten in der neuen Gesamtstruktur, das Verwenden von Sicherheitsgruppen aus der neuen Gesamtstruktur als Clientsicherheitsgruppe, Ausführen von Remoteaufrufen (WinRM, RPC) von Computern in der neuen Gesamtstruktur und Authentifizieren von Remoteclients in der neuen Gesamtstruktur.  
  
## <a name="plan-remote-access-administrator-permissions"></a>Planen der Administratorberechtigungen für den Remotezugriff  
Beim Konfigurieren des Remotezugriffs werden Gruppenrichtlinienobjekte aktualisiert und manchmal in den einzelnen Domänen erstellt, die RAS-Server oder Remotezugriffsclients enthalten. In einer Umgebung mit mehreren Gesamtstrukturen muss der Remotezugriffsadministrator genau wie in einer Umgebung mit einer Gesamtstruktur über Berechtigungen zum Schreiben und Ändern von DirectAccess-Gruppenrichtlinienobjekten und ihren Sicherheitsfiltern verfügen. Optional muss er Berechtigungen zum Erstellen von Links für die DirectAccess-Gruppenrichtlinienobjekte in allen betroffenen Gesamtstrukturen besitzen. Diese Berechtigungen sind unabhängig von der Gesamtstruktur erforderlich, zu der der Remotezugriffsadministrator gehört.  
  
Darüber hinaus muss es sich beim Remotezugriffsadministrator um einen lokalen Administrator für alle RAS-Server handeln, einschließlich der RAS-Server in der neuen Gesamtstruktur, die als Einstiegspunkte zur ursprünglichen Remotezugriffsbereitstellung hinzugefügt werden.  
  
## <a name="ClientSG"></a>Planen von clientsicherheitsgruppen  
Sie müssen mindestens eine Sicherheitsgruppe in der neuen Gesamtstruktur für DirectAccess-Clientcomputer in der neuen Gesamtstruktur konfigurieren. Eine einzelne Sicherheitsgruppe kann keine Konten aus verschiedenen Gesamtstrukturen enthalten.  
  
> [!NOTE]  
> -   DirectAccess erfordert mindestens ein Windows 10&reg; oder Windows&reg; 8-clientsicherheitsgruppe für jede Gesamtstruktur. Allerdings empfiehlt es sich um ein Windows 10 oder Windows 8-clientsicherheitsgruppe für jede Domäne, die Windows 10 oder Windows 8-Clients enthält.  
> -   Wenn mehrere Standorte aktiviert ist, wird DirectAccess erfordert mindestens Windows 7&reg; -clientsicherheitsgruppe pro Gesamtstruktur für jeden DirectAccess-Einstiegspunkt in die Windows 7-Clientcomputern unterstützt werden. Allerdings empfiehlt es sich um einen separaten Windows 7-clientsicherheitsgruppe für jeden Einstiegspunkt für jede Domäne zu erhalten, die Windows 7-Clients enthält.  
>   
> Damit DirectAccess auf Clientcomputer in zusätzlichen Domänen angewendet wird, müssen Client-Gruppenrichtlinienobjekte in diesen Domänen erstellt werden. Durch das Hinzufügen von Sicherheitsgruppen wird das Schreiben neuer Client-Gruppenrichtlinienobjekte für die neuen Domänen ausgelöst. Wenn Sie der Liste der Sicherheitsgruppen für DirectAccess-Clients eine neue Sicherheitsgruppe aus einer neuen Domäne hinzufügen, wird daher automatisch ein Client-Gruppenrichtlinienobjekt in der neuen Domäne erstellt. Clientcomputer in der neuen Domäne erhalten die DirectAccess-Einstellungen über das Client-Gruppenrichtlinienobjekt.  
>   
> Wenn Sie einer vorhandenen Sicherheitsgruppe, die bereits als Sicherheitsgruppe für DirectAccess-Clients konfiguriert ist, einen Client aus einer neuen Domäne hinzufügen, wird das Client-Gruppenrichtlinienobjekt nicht automatisch von DirectAccess in der neuen Domäne erstellt. Der Client in der neuen Domäne erhält nicht die DirectAccess-Einstellungen und kann daher keine Verbindung mithilfe von DirectAcecss herstellen.  
  
## <a name="plan-certification-authorities"></a>Planen von Zertifizierungsstellen  
Ist die DirectAccess-Bereitstellung für die Verwendung der Authentifizierung mit Einmalkennwörtern (One-Time Password, OTP) konfiguriert, enthält jede Gesamtstruktur die gleichen Signaturzertifikatvorlagen. Diese Vorlagen enthalten jedoch unterschiedliche OID-Werte. Dies führt dazu, dass die Gesamtstrukturen nicht als eine Konfigurationseinheit konfiguriert werden können. Um dieses Problem zu beheben, und Konfigurieren von Einmalkennwörtern in einer Umgebung mit mehreren Gesamtstrukturen, finden Sie im Abschnitt "Configure OTP in einer Bereitstellung mit mehreren Gesamtstrukturen" im Thema [Konfigurieren einer Bereitstellung mit mehreren Gesamtstrukturen](Configure-a-Multi-Forest-Deployment.md).  
  
Bei der Verwendung der IPsec-Computerzertifikatauthentifizierung muss auf allen Client- und Servercomputern (unabhängig von der Gesamtstruktur, zu der sie gehören) ein von derselben Stamm- oder Zwischenzertifizierungsstelle ausgestelltes Computerzertifikat vorhanden sein.  
  
## <a name="plan-otp-exemptions"></a>Planen von OTP-Ausnahmen  
Bei der Verwendung der DirectAccess-OTP-Authentifizierung ist die Sicherheitsgruppe für OTP-Ausnahmen auf Benutzer einer einzelnen Gesamtstruktur beschränkt. Dies liegt daran, dass jede Sicherheitsgruppe nur Benutzer aus einer einzelnen Gesamtstruktur enthalten und nur eine Sicherheitsgruppe konfiguriert werden kann.  
  


