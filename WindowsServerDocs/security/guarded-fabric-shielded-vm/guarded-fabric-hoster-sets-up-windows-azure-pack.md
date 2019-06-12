---
title: 'Abgeschirmte VMs: Hosting-Anbieter richtet Windows Azure Pack ein'
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d528c689-58b0-425c-9740-25e2553ed689
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 156832087bc7af0c95a92cab9a0c1501264d47a5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447504"
---
# <a name="shielded-vms---hosting-service-provider-sets-up-windows-azure-pack"></a>Abgeschirmte VMs: Hosting-Anbieter richtet Windows Azure Pack ein

In diesem Thema wird beschrieben, wie einem Hostingdienstanbieter Windows Azure Pack konfigurieren kann, damit Mandanten ihn verwenden können, um abgeschirmte VMs bereitzustellen. Windows Azure Pack ist ein Webportal, das erweitert die Funktionalität von System Center Virtual Machine Manager können Mandanten bereitstellen und verwalten ihre eigenen VMs über eine einfache Web-Schnittstelle. Windows Azure Pack unterstützt abgeschirmte virtuelle Computer vollständig und erleichtert es auch für Ihre Mandanten erstellen und verwalten ihre geschützte Datendateien.

Um zu verstehen, wie in diesem Thema in den gesamten Vorgang der Bereitstellung von abgeschirmten VMs passt, finden Sie unter [Service Provider-Konfigurationsschritte für das Hosten von überwachten Hosts und abgeschirmte VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md).

## <a name="setting-up-windows-azure-pack"></a>Einrichten von Windows Azure Pack

Führen Sie die folgenden Aufgaben zum Einrichten von Windows Azure Pack in Ihrer Umgebung ein:

1. Schließen Sie die Konfiguration von System Center 2016 – Virtual Machine Manager (VMM) für Ihr Fabric hosten. Dies beinhaltet das Einrichten von VM-Vorlagen und einer VM-Cloud, die über Windows Azure Pack verfügbar gemacht werden:

    [Szenario – Bereitstellen von überwachten Hosts und geschützten virtuellen Maschinen in VMM](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview)

2. Installieren Sie und konfigurieren Sie System Center 2016 – Service Provider Foundation (SPF). Diese Software ermöglicht Windows Azure Pack für die Kommunikation mit Ihrer VMM-Server:

    [Bereitstellen von Service Provider Foundation - SPF](https://technet.microsoft.com/system-center-docs/spf/deploy/deploy-spf)

3. Installieren Sie Windows Azure Pack und konfigurieren sie für die Kommunikation mit SPF:

    - [Installieren von Windows Azure Pack](#install-windows-azure-pack) (in diesem Thema)
    - [Konfigurieren von Windows Azure Pack](#configure-windows-azure-pack) (in diesem Thema)

4. Erstellen Sie eine oder mehrere hostingpläne in Windows Azure Pack, um die Mandanten den Zugriff auf Ihre VM-Clouds ermöglichen:

    [Erstellen eines Plans im Windows Azure Pack](#create-a-plan-in-windows-azure-pack) (in diesem Thema)

## <a name="install-windows-azure-pack"></a>Installieren Sie Windows Azure Pack

Installieren und Konfigurieren von Windows Azure Pack (WAP) auf dem Computer, in dem Sie das Hosten des Webportals für Ihre Mandanten möchten. Dieser Computer müssen möglicherweise den SPF-Server nicht erreichen und Ihre Mandanten erreichbar sein.

1.  Überprüfen der [WAP-Systemanforderungen](https://technet.microsoft.com/library/dn296442.aspx) herunter, und Installieren der [erforderliche Software](https://technet.microsoft.com/library/dn469335.aspx).

2.  Herunterladen und Installieren der [Webplattform-Installer](https://www.microsoft.com/web/downloads/platform.aspx). Wenn der Computer nicht mit dem Internet verbunden ist, führen Sie die [Anweisungen zur offline-Installation](http://www.iis.net/learn/install/web-platform-installer/web-platform-installer-v4-command-line-webpicmdexe-rtw-release).

3.  Öffnen Sie den Webplattform-Installer, und suchen **Windows Azure Pack: Portal und API Express** unter der **Produkte** Registerkarte. Klicken Sie auf **hinzufügen**, klicken Sie dann **installieren** am unteren Rand des Fensters.

4.  Führen Sie die weiteren Schritte der Installation aus. Nach Abschluss der Installation, die die Konfigurationswebsite (*https://&lt;Wapserver&gt;: 30101 /* ) in Ihrem Webbrowser wird geöffnet. Auf dieser Website Informationen zu Ihrer SQLServer und abzuschließen Sie WAP Konfiguration.

Hilfe zu Windows Azure Pack einrichten, finden Sie unter [Installieren einer expressbereitstellung von Windows Azure Pack](https://technet.microsoft.com/dn296439.aspx).

> [!NOTE]
> Wenn Sie bereits über Windows Azure Pack in Ihrer Umgebung ausführen, können Sie Ihre vorhandene Installation verwenden. Für die Arbeit mit den neuesten abgeschirmte VM-Funktionen, jedoch müssen Sie so aktualisieren die Installation auf mindestens Update Rollup 10.

### <a name="configure-windows-azure-pack"></a>Konfigurieren Sie Windows Azure Pack

Bevor Sie Windows Azure Pack verwenden, sollten Sie es installiert und konfiguriert für Ihre Infrastruktur noch.

1.  Navigieren Sie auf das Windows Azure Pack-Verwaltungsportal unter *https://&lt;Wapserver&gt;: 30091*, und melden Sie sich mit Ihren Administratoranmeldeinformationen.

2.  Klicken Sie im linken Bereich auf **VM-Clouds**.

3.  Verbinden von Windows Azure Pack mit der Service Provider Foundation-Instanz, indem Sie auf **System Center Service Provider Foundation registrieren**. Sie benötigen die URL für Service Provider Foundation, sowie einen Benutzernamen und ein Kennwort angeben.

    ![System Center Service Provider Foundation registrieren](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-01-register-spf.png)

4.  Danach sollten Sie können Sie die VM-Clouds, die in der VMM-Umgebung eingerichtet sein. Stellen Sie sicher, dass Sie mindestens eine VM-Cloud verfügen, unterstützt von VMs, die für WAP vor dem Fortfahren abgeschirmten.

### <a name="create-a-plan-in-windows-azure-pack"></a>Erstellen eines Plans im Windows Azure Pack

Zum Erstellen von VMs in WAP-Mandanten zu ermöglichen, müssen Sie zuerst einen hostingplan erstellen, den Mandanten abonnieren können. Pläne werden die zulässigen VM-Clouds, Vorlagen, Netzwerke und abrechnungseinheiten für Ihre Mandanten definieren.

1. Klicken Sie auf den unteren Bereich des Portals auf **+ neu** &gt; **planen** &gt; **erstellen planen**.

2. Wählen Sie im ersten Schritt des Assistenten einen Namen für Ihren Plan aus. Dies ist der Name, die Ihren Mandanten beim Abonnieren angezeigt werden.

3. Wählen Sie im zweiten Schritt **CLOUDS für virtuelle Computer** als einer der Dienste im Plan anbieten.

4. Überspringen Sie den Schritt zum Auswählen von Add-ons für den Plan an.

5. Klicken Sie auf **OK** (Häkchen) aus, um den Plan zu erstellen. Obwohl dies den Plan erstellt haben, ist es nicht bereits in einem konfigurierten Zustand.

   ![Pläne in Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-02-create-plan.png)

6. Um zu beginnen, konfigurieren den Plan, klicken Sie auf seinen Namen.

7. Klicken Sie auf der nächsten Seite unter **plandienste**, klicken Sie auf **Clouds für virtuelle Computer**. Daraufhin wird die Seite, in denen Sie Kontingente für diesen Plan konfigurieren können.

8. Klicken Sie unter **grundlegende**, wählen Sie die VMM-Verwaltungsserver und die VM-Cloud, die Sie für Ihre Mandanten anbieten möchten. Clouds, die abgeschirmte VMs bieten können mit angezeigt werden **(Abschirmung unterstützt)** neben ihrem Namen.

9. Wählen Sie die Kontingente, die Sie in diesem Plan anwenden möchten. (Z. B. Grenzwerte für CPU-Kern und RAM-Auslastung). Stellen Sie sicher, dass die **können virtuelle Computer werden von geschützten** Kontrollkästchen.

   ![Einstellungen für Clouds für virtuelle Computer in Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-03-virtual-machine-clouds.png)
    
10. Suchen Sie im Abschnitt **Vorlagen**, und wählen Sie dann eine oder mehrere Vorlagen für Ihren Mandanten anbieten. Sie bieten sowohl abgeschirmte und nicht abgeschirmten Vorlagen für Mandanten, aber einer geschützten Vorlage muss Mandanten über End-to-End-zusicherungen über die Integrität der VM und ihre Geheimnisse gewähren angeboten werden.

11. In der **Netzwerke** Abschnitt fügen Sie ein oder mehrere Netzwerke für Ihre Mandanten hinzu.

12. Nach dem Festlegen einer anderen Einstellungen oder Kontingente für den Plan an, klicken Sie auf **speichern** am unteren Rand.

13. AT oben links auf dem Bildschirm, klicken Sie auf den Pfeil, um Sie nutzen zurück an die **planen** Seite.

14. Ändern Sie am unteren Rand des Bildschirms, den Plan wird **Private** zu **öffentliche** , damit Mandanten den Plan abonnieren können.

    ![Ändern des Zugriffs für einen Plan in Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-04-change-access.png)

    An diesem Punkt wird Windows Azure Pack konfiguriert ist, und Mandanten werden in der Lage, abonnieren Sie den Plan, den Sie gerade erstellt haben, und geschützte VMs bereitstellen. Zusätzliche Schritte, die Mandanten ausführen müssen, finden Sie unter [abgeschirmter VMs für Mandanten – Bereitstellen eines abgeschirmten virtuellen Computers mit Windows Azure Pack](guarded-fabric-shielded-vm-windows-azure-pack.md).

## <a name="see-also"></a>Siehe auch

- [Hosten von Service Provider-Konfigurationsschritte für die überwachten Hosts und abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
