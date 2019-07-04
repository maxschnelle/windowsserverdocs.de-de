---
title: Empfehlungen für die Umstellung auf Windows Server 2016
description: Empfehlungen für die Umstellung auf Windows Server 2016.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 10/18/2016
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 74aa1da3-7076-4a1f-ad5b-9e17bd46dba2
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 08a92188446d018edd36a638abb30745721bd601
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "63687482"
---
# <a name="recommendations-for-moving-to-windows-server-2016"></a>Empfehlungen für die Umstellung auf Windows Server 2016

>Gilt für: Windows Server 2016


|Im Folgenden werden die Betriebssysteme aufgeführt:|Windows Server 2012 R2 oder Windows Server 2012|Windows Server 2008 R2 oder Windows Server 2008|  
|-------------------|----------|--------------|--------------|---------------------------------------|  
|**Windows Server-Rolleninfrastruktur**|Wählen Sie abhängig vom [Leitfaden für bestimmte Rollen](https://technet.microsoft.com/windowsserver/jj554790) entweder Upgrade oder Migration aus.|– Um die neuen Features in Windows Server 2016 nutzen zu können, stellen Sie neue Hardware bereit, oder installieren Sie Windows Server 2016 auf einem virtuellen Computer auf einem vorhandenen Host. Einige neue Features funktionieren am besten auf einem physischen Windows Server 2016-Host mit Hyper-V. <br>– Befolgen Sie den [Leitfaden für bestimmte Rollen](https://technet.microsoft.com/windowsserver/jj554790).|
|**Microsoft-Serververwaltung und Anwendungsworkloads**|– Anwendungsupgrades sollten die *Migration* zu Windows Server 2016 umfassen. Informationen hierzu finden Sie in der [Kompatibilitätsliste](Server-Application-Compatibility.md). <br>– Bei reinen Upgrades auf Windows Server 2016 (d.h. ohne Anwendungsupgrades) sollten Sie die anwendungsspezifische Anleitung verwenden.|– Um die neuen Features in Windows Server 2016 nutzen zu können, stellen Sie neue Hardware bereit, oder installieren Sie Windows Server 2016 auf einem virtuellen Computer auf einem vorhandenen Host. Einige neue Features funktionieren am besten auf einem physischen Windows Server 2016-Host mit Hyper-V. Befolgen Sie ggf. die Migrationshandbücher. <br>– Oder behalten Sie Ihr aktuelles Betriebssystem bei, und führen Sie das Programm auf einem virtuellen Computer auf einem Windows Server 2016-Host oder unter Microsoft Azure aus. Wenden Sie sich an Ihren EA-Händler, TAM oder an Microsoft, um erweiterte Supportoptionen über [Software Assurance](https://www.microsoft.com/en-us/Licensing/licensing-programs/software-assurance-default.aspx) zu erhalten.|
|**ISV-Anwendungsworkloads**|– Bei Upgrades auf Windows Server 2016 sollte die anwendungsspezifische Anleitung verwendet werden. <br>– Weitere Informationen zur Kompatibilität von Windows Server mit nicht von Microsoft stammenden Anwendungen finden Sie im Portal [Windows Server Logo Certification](https://msdn.microsoft.com/enterprisecloudcertified).|– Um die neuen Features in Windows Server 2016 nutzen zu können, stellen Sie neue Hardware bereit, oder installieren Sie Windows Server 2016 auf einem virtuellen Computer auf einem vorhandenen Host. Einige neue Features funktionieren am besten auf einem physischen Windows Server 2016-Host mit Hyper-V. Befolgen Sie ggf. die Migrationshandbücher. <br>– Oder behalten Sie Ihr aktuelles Betriebssystem bei, und führen Sie das Programm auf einem virtuellen Computer auf einem Windows Server 2016-Host oder unter Microsoft Azure aus. Wenden Sie sich an Ihren EA-Händler, TAM oder an Microsoft, um erweiterte Supportoptionen über [Software Assurance](https://www.microsoft.com/en-us/Licensing/licensing-programs/software-assurance-default.aspx) zu erhalten.|
|**Benutzerdefinierte Anwendungsworkloads**|– Ziehen Sie bezüglich der Kompatibilität mit Windows Server 2016 und für Upgradeanweisungen Anwendungsentwickler zurate. <br>– Nutzen Sie vor dem Wechseln Microsoft Azure zum Testen der Anwendung unter Windows Server 2016. <br>– Eine vollständige Übersicht über die Optionen finden Sie im nächsten Abschnitt.|– Ziehen Sie bezüglich der Kompatibilität mit Windows Server 2016 und für Upgradeanweisungen Ihre Anwendungsentwickler zurate. <br>– Nutzen Sie vor dem Wechseln Microsoft Azure zum Testen Ihrer Anwendung unter Windows Server 2016. <br>– Um die neuen Features in Windows Server 2016 nutzen zu können, stellen Sie neue Hardware bereit, oder installieren Sie Windows Server 2016 auf einem virtuellen Computer auf einem vorhandenen Host. Einige neue Features funktionieren am besten auf einem physischen Windows Server 2016-Host mit Hyper-V. <br>– Eine vollständige Übersicht über die Optionen finden Sie im nächsten Abschnitt.|

## <a name="complete-options-for-moving-servers-running-custom-or-in-house-applications-on-older-versions-of-windows-server-to-windows-server-2016"></a>Vollständige Übersicht über die Optionen für die Migration von Servern mit benutzerdefinierten oder „internen“ Anwendungen unter älteren Versionen von Windows Server zu Windows Server 2016

Es gibt jetzt mehr Optionen als jemals zuvor, die Ihnen und Ihren Kunden die Nutzung der Features in Windows Server 2016 erleichtern und die Auswirkung auf Ihre aktuellen Dienste und Workloads minimieren.

- Testen Sie das neueste Betriebssystem mit Ihren Anwendungen, indem Sie die Evaluierungsversion von [Windows Server](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016) herunterladen und in Ihrer lokalen Umgebung testen. Nachdem Sie die Tests abgeschlossen und sich von der Qualität überzeugt haben, können Sie eine einfache Lizenzkonvertierung mit einem Lizenzschlüssel für die Verkaufsversion ausführen (Neustart erforderlich).

- Sie können auch eine Evaluierungsversion von [Microsoft Azure](https://azure.microsoft.com) zu Testzwecken verwenden, um sicherzustellen, dass Ihre benutzerdefinierte Anwendung auf dem neuesten Serverbetriebssystem ausgeführt werden kann. Nachdem Sie die Tests abgeschlossen und sich von der Qualität überzeugt haben, führen Sie in Ihrer lokalen Umgebung die [Migration Ihres Systems zur neuesten Version von Windows Server](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade#upgrade) aus. 

- Alternativ können Sie, nachdem Sie die Tests abgeschlossen und sich von der Qualität überzeugt haben, [Microsoft Azure](https://azure.microsoft.com) als dauerhaften Speicherort für Ihre benutzerdefinierte Anwendung oder Dienste verwenden. Dadurch kann der alte Server verfügbar bleiben, bis Sie bereit sind, zum neuen Server in Azure zu wechseln.

    - Wenn Sie bereits über Software Assurance für Windows Server verfügen, sparen Sie Geld, indem Sie die Bereitstellung mit dem [Microsoft Azure-Vorteil bei Hybridnutzung](https://azure.microsoft.com/pricing/hybrid-use-benefit/) vornehmen. 

- In den meisten Fällen kann [Microsoft Azure](https://azure.microsoft.com) verwendet werden, um dieselbe Anwendung auf der aktuell ausgeführten, älteren Version von Windows Server zu hosten. Migrieren Sie die Anwendung und den Workload zu einem virtuellen Computer mit dem Betriebssystem Ihrer Wahl unter Verwendung von [Azure Marketplace](https://azure.microsoft.com/marketplace/)-Images.

    - Wenn Sie bereits über Software Assurance für Windows Server verfügen, sparen Sie Geld, indem Sie die Bereitstellung mit dem [Microsoft Azure-Vorteil bei Hybridnutzung](https://azure.microsoft.com/pricing/hybrid-use-benefit/) vornehmen. 

- Mit dem [Software Assurance](https://www.microsoft.com/en-us/Licensing/licensing-programs/software-assurance-default.aspx)-Programm für Windows Server können Sie von neuen Versionsrechten profitieren. Sie profitieren nicht nur von einer Reihe zahlreicher weiterer Vorteile, sondern können, wenn der Zeitpunkt gekommen ist, Server mit Software Assurance auf die neueste Version von Windows Server aktualisieren, ohne eine neue Lizenz erwerben zu müssen. 

## <a name="additional-resources"></a>Zusätzliche Ressourcen

- [In Windows Server 2016 entfernte oder veraltete Features](deprecated-features.md)
- Allgemeine Optionen für Serverupgrade und -migration finden Sie auf [Upgrade- und Konvertierungsoptionen für Windows Server 2016](Supported-Upgrade-Paths.md).
- Weitere Informationen zu Produktlebenszyklus und Supportstufen finden Sie unter [Support Lifecycle-Richtlinie – FAQ](https://support.microsoft.com/help/17140/support-lifecycle-policy-faq).

