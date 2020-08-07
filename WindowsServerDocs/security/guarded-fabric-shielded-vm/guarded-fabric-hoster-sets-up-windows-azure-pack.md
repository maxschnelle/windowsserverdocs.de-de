---
title: 'Abgeschirmte VMs: Hosting-Anbieter richtet Windows Azure Pack ein'
ms.topic: article
ms.assetid: d528c689-58b0-425c-9740-25e2553ed689
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 7e62b5dab69676e15494ff531ffe0fce0e550c1a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970087"
---
# <a name="shielded-vms---hosting-service-provider-sets-up-windows-azure-pack"></a>Abgeschirmte VMs: Hosting-Anbieter richtet Windows Azure Pack ein

In diesem Thema wird beschrieben, wie ein hostingdienstanbieter Windows Azure Pack konfigurieren kann, damit Mandanten ihn zum Bereitstellen von abgeschirmten VMS verwenden können. Windows Azure Pack ist ein Webportal, das die Funktionalität von System Center Virtual Machine Manager erweitert, damit Mandanten ihre eigenen VMS über eine einfache Weboberfläche bereitstellen und verwalten können. Windows Azure Pack werden abgeschirmte VMS vollständig unterstützen und die Erstellung und Verwaltung Ihrer geschützten Datendateien für Ihre Mandanten noch einfacher.

Informationen dazu, wie sich dieses Thema in den Gesamtprozess der Bereitstellung von abgeschirmten VMS einfügt, finden Sie unter [Hosten von Dienstanbietern Konfigurationsschritte für geschützte Hosts und abgeschirmte VMS](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md).

## <a name="setting-up-windows-azure-pack"></a>Einrichten von Windows Azure Pack

Sie führen die folgenden Aufgaben aus, um Windows Azure Pack in Ihrer Umgebung einzurichten:

1. Vervollständigen Sie die Konfiguration von System Center 2016-Virtual Machine Manager (VMM) für Ihr hostingfabric. Dies umfasst das Einrichten von VM-Vorlagen und eine VM-Cloud, die über Windows Azure Pack verfügbar gemacht wird:

    [Szenario: Bereitstellen von überwachten Hosts und geschützten virtuellen Maschinen in VMM](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview)

2. Installieren und Konfigurieren von System Center 2016-Service Provider Foundation (SPF). Diese Software ermöglicht Windows Azure Pack die Kommunikation mit Ihren VMM-Servern:

    [Bereitstellen von Service Provider Foundation-SPF](https://technet.microsoft.com/system-center-docs/spf/deploy/deploy-spf)

3. Installieren Sie Windows Azure Pack, und konfigurieren Sie ihn für die Kommunikation mit SPF:

    - [Installieren von Windows Azure Pack](#install-windows-azure-pack) (in diesem Thema)
    - [Konfigurieren von Windows Azure Pack](#configure-windows-azure-pack) (in diesem Thema)

4. Erstellen Sie einen oder mehrere hostingpläne in Windows Azure Pack, um Mandanten den Zugriff auf Ihre VM-Clouds zu ermöglichen:

    [Erstellen eines Plans in Windows Azure Pack](#create-a-plan-in-windows-azure-pack) (in diesem Thema)

## <a name="install-windows-azure-pack"></a>Installieren von Windows Azure Pack

Installieren und konfigurieren Sie Windows Azure Pack (WAP) auf dem Computer, auf dem Sie das Webportal für Ihre Mandanten hosten möchten. Dieser Computer muss in der Lage sein, den SPF-Server zu erreichen und für Ihre Mandanten erreichbar zu sein.

1.  Überprüfen der [WAP-Systemanforderungen](https://technet.microsoft.com/library/dn296442.aspx) und Installieren der [erforderlichen Software](https://technet.microsoft.com/library/dn469335.aspx).

2.  Herunterladen und Installieren des [Webplattform-Installers](https://www.microsoft.com/web/downloads/platform.aspx). Wenn der Computer nicht mit dem Internet verbunden ist, befolgen Sie die [Anweisungen zur Offline Installation](https://www.iis.net/learn/install/web-platform-installer/web-platform-installer-v4-command-line-webpicmdexe-rtw-release).

3.  Öffnen Sie den Webplattform-Installer, und suchen Sie nach **Windows Azure Pack: Portal und API Express** auf der Registerkarte **Produkte** . Klicken Sie auf **Hinzufügen**, und **Installieren** Sie dann am unteren Rand des Fensters.

4.  Führen Sie die weiteren Schritte der Installation aus. Nachdem die Installation abgeschlossen ist, wird die Konfigurations Website (*https:// &lt; wapserver &gt; : 30101/*) in Ihrem Webbrowser geöffnet. Geben Sie auf dieser Website Informationen zu Ihrem SQL-Server an, und schließen Sie die Konfiguration von WAP ab.

Hilfe zum Einrichten von Windows Azure Pack finden Sie unter [Installieren einer Express-Bereitstellung Windows Azure Pack](https://technet.microsoft.com/dn296439.aspx).

> [!NOTE]
> Wenn Sie Windows Azure Pack bereits in Ihrer Umgebung ausgeführt haben, können Sie die vorhandene-Installation verwenden. Um mit den neuesten geschützten VM-Features arbeiten zu können, müssen Sie jedoch die Installation auf mindestens Updaterollup 10 aktualisieren.

### <a name="configure-windows-azure-pack"></a>Konfigurieren von Windows Azure Pack

Bevor Sie Windows Azure Pack verwenden, sollten Sie es bereits installiert und für Ihre Infrastruktur konfiguriert haben.

1.  Navigieren Sie zum Windows Azure Pack Admin-Portal unter *https:// &lt; wapserver &gt; : 30091*, und melden Sie sich dann mit Ihren Administrator Anmelde Informationen an.

2.  Klicken Sie im linken Bereich auf **VM-Clouds**.

3.  Verbinden Sie Windows Azure Pack mit der Service Provider Foundation Instanz, indem Sie auf **System Center Service Provider Foundation registrieren**klicken. Sie müssen die URL für Service Provider Foundation sowie einen Benutzernamen und ein Kennwort angeben.

    ![System Center Service Provider Foundation registrieren](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-01-register-spf.png)

4.  Nachdem der Vorgang abgeschlossen ist, sollten Sie in der Lage sein, die VM-Clouds in Ihrer VMM-Umgebung einzurichten. Stellen Sie sicher, dass Sie mindestens eine VM-Cloud haben, die abgeschirmte VMS unterstützt, die für WAP verfügbar sind

### <a name="create-a-plan-in-windows-azure-pack"></a>Erstellen eines Plans in Windows Azure Pack

Damit Mandanten VMs in WAP erstellen können, müssen Sie zuerst einen Hostingplan erstellen, den Mandanten abonnieren können. Pläne definieren die zulässigen VM-Clouds,-Vorlagen,-Netzwerke und-Abrechnungs Entitäten für Ihre Mandanten.

1. Klicken Sie im unteren Bereich des Portals auf **+ neuer** &gt; **Plan** &gt; **Create Plan**.

2. Wählen Sie im ersten Schritt des Assistenten einen Namen für den Plan aus. Dies ist der Name, den Ihre Mandanten beim Abonnieren sehen.

3. Wählen Sie im zweiten Schritt die Option VM- **Clouds** als einer der Dienste aus, die im Plan angeboten werden sollen.

4. Überspringen Sie den Schritt zum Auswählen von Add-ons für den Plan.

5. Klicken Sie auf **OK** (Häkchen), um den Plan zu erstellen. Obwohl dies den Plan erstellt, befindet er sich noch nicht in einem konfigurierten Zustand.

   ![Pläne in Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-02-create-plan.png)

6. Um mit der Konfiguration des Plans zu beginnen, klicken Sie auf seinen Namen.

7. Klicken Sie auf der nächsten Seite unter **Plan Dienste**auf VM- **Clouds**. Dadurch wird die Seite geöffnet, auf der Sie Kontingente für diesen Plan konfigurieren können.

8. Wählen Sie unter **Basic**den VMM-Verwaltungs Server und die VM-Cloud aus, die Sie Ihren Mandanten anbieten möchten. Clouds, die abgeschirmte VMS anbieten können, werden mit **(Schutz unterstützt)** neben dem Namen angezeigt.

9. Wählen Sie die Kontingente aus, die Sie in diesem Plan anwenden möchten. (Z. b. Grenzwerte für CPU-Kern und RAM-Auslastung). Vergewissern Sie sich, dass das Kontrollkästchen **Virtual Machines als geschützt zulassen** aktiviert ist.

   ![Einstellungen für Clouds für virtuelle Computer in Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-03-virtual-machine-clouds.png)

10. Scrollen Sie nach unten zum Abschnitt **Vorlagen**, und wählen Sie dann eine oder mehrere Vorlagen aus, die ihren Mandanten angeboten werden sollen. Sie können Mandanten sowohl abgeschirmte als auch unsadierte Vorlagen anbieten, aber es muss eine geschützte Vorlage angeboten werden, um Mandanten eine End-to-End-Zusicherung über die Integrität der VM und ihrer geheimen Schlüssel zu geben.

11. Fügen Sie im Abschnitt " **Netzwerke** " ein oder mehrere Netzwerke für Ihre Mandanten hinzu.

12. Nachdem Sie andere Einstellungen oder Kontingente für den Plan festgelegt haben, klicken Sie unten auf **Speichern** .

13. Klicken Sie oben links auf dem Bildschirm auf den Pfeil, um zur Seite " **Plan** " zurückzukehren.

14. Ändern Sie am unteren Bildschirmrand den Plan von **Privat** in **öffentlich** , damit Mandanten den Plan abonnieren können.

    ![Ändern des Zugriffs für einen Plan in Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-host-azure-pack-04-change-access.png)

    An diesem Punkt ist Windows Azure Pack konfiguriert, und Mandanten können den soeben erstellten Plan abonnieren und abgeschirmte VMS bereitstellen. Weitere Schritte, die Mandanten ausführen müssen, finden Sie unter [abgeschirmte VMs für Mandanten: Bereitstellen einer abgeschirmten VM mithilfe von Windows Azure Pack](guarded-fabric-shielded-vm-windows-azure-pack.md).

## <a name="additional-references"></a>Weitere Verweise

- [Geschützte Hosts und abgeschirmte VMs: Konfigurationsschritte für Hosting-Anbieter](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
