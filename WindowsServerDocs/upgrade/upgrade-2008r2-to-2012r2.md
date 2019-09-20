---
title: Aktualisieren von Windows Server 2008 R2 auf Windows Server 2012 R2 | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie ein direktes Upgrade von Windows Server 2008 R2 auf Windows Server 2012 R2 durchführen.
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: d5051239f7269eb4b6361187121ac960e06f6d9e
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/19/2019
ms.locfileid: "71125080"
---
# <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>Aktualisieren von Windows Server 2008 R2 auf Windows Server 2012 R2

Wenn Sie dieselbe Hardware und alle Server Rollen beibehalten möchten, die Sie bereits eingerichtet haben, ohne den Server zu vereinfachen, sollten Sie ein direktes Upgrade durchführen. Ein direktes Upgrade ermöglicht es Ihnen, von einem älteren Betriebssystem zu einem neueren zu wechseln, während Ihre Einstellungen, Server Rollen und Daten unverändert bleiben. Dieser Artikel unterstützt Sie bei der Umstellung von Windows Server 2008 R2 auf Windows Server 2012 R2.

Wenn Sie ein Upgrade auf Windows Server 2019 durchführen möchten, verwenden Sie dieses Thema zunächst für ein Upgrade auf Windows Server 2012 R2, und führen Sie dann ein [Upgrade von Windows Server 2012 R2 auf Windows Server 2019 aus](upgrade-2012r2-to-2019.md).

## <a name="before-you-begin-your-in-place-upgrade"></a>Bevor Sie mit dem direkten Upgrade beginnen

Bevor Sie mit dem Windows Server-Upgrade beginnen, wird empfohlen, dass Sie Informationen zu Diagnose-und Problem Behandlungszwecken von ihren Geräten sammeln. Da diese Informationen nur für die Verwendung vorgesehen sind, wenn das Upgrade fehlschlägt, müssen Sie sicherstellen, dass Sie die Informationen an einem Ort speichern, an dem Sie von Ihrem Gerät aus gelangen können.

### <a name="to-collect-your-info"></a>So erfassen Sie Ihre Informationen

1. Öffnen Sie eine Eingabeaufforderung, navigieren `c:\Windows\system32`Sie zu, und geben Sie dann **Systeminfo. exe**ein.

2. Kopieren, einfügen und speichern Sie die resultierenden Systeminformationen an einem beliebigen Speicherort Ihres Geräts.

3. Geben Sie in der Eingabeaufforderung **ipconfig/all** ein, kopieren Sie die resultierenden Konfigurationsinformationen, und fügen Sie Sie an den gleichen Speicherort wie oben ein.

4. Öffnen Sie den Registrierungs-Editor, navigieren Sie zu HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion Hive, kopieren Sie die Windows Server-Datei **BuildLabEx** (Version) und **EditionID** (Edition), und fügen Sie Sie an denselben Speicherort wie oben ein.

Nachdem Sie alle Ihre Windows Server-bezogenen Informationen gesammelt haben, empfehlen wir Ihnen dringend, Ihr Betriebssystem, Ihre apps und Ihre virtuellen Computer zu sichern. Sie müssen auch alle virtuellen Maschinen, die derzeit auf dem Server ausgeführt werden, **herunter**fahren, **schnell migrieren**oder **Live migrieren** . Während der direkten Aktualisierung können keine virtuellen Computer ausgeführt werden.

## <a name="to-perform-the-upgrade"></a>So führen Sie das Upgrade aus

1. Stellen Sie sicher, dass der **BuildLabEx** -Wert besagt, dass Sie Windows Server 2008 R2 ausführen.

2. Suchen Sie nach dem Windows Server 2012 R2-Setup Medium, und wählen Sie dann **Setup. exe**aus.

    ![Windows-Explorer mit der Datei "Setup. exe"](media/upgrade-2008r2-2012r2/setup-2012r2.png)

3. Wählen Sie **Ja** aus, um den Setup Vorgang zu starten.

    ![Benutzerkontensteuerung, die die Berechtigung zum Starten des Setups anfordert](media/upgrade-2008r2-2012r2/start-setup-uac-box.png)

4. Wählen Sie auf dem Bildschirm Windows Server 2012 R2 die Option **jetzt installieren**aus.

5. Wählen Sie für mit dem Internet verbundene Geräte die Option online schalten, **um Updates jetzt zu installieren (empfohlen)** aus.

    ![Bildschirm, der online geschaltet werden soll, um wichtige Windows-Updates zu erhalten](media/upgrade-2008r2-2012r2/imp-updates-win-setup.png)

6. Wählen Sie die Windows Server 2012 R2-Edition aus, die Sie installieren möchten, und klicken Sie dann auf **weiter**.

    ![Bildschirm zum Auswählen der zu installierende Windows Server 2012 R2-Edition](media/upgrade-2008r2-2012r2/select-os-edition.png)

7. Wählen Sie **Ich akzeptiere die Lizenzbedingungen** aus, um die Bedingungen Ihres Lizenzierungs Vertrags auf Grundlage ihres Verteilungs Kanals (z. b. Verkaufs-, Volumenlizenz, OEM, ODM usw.) zu akzeptieren, und klicken Sie dann auf **weiter**.

    ![Bildschirm zur Annahme Ihres Lizenzvertrags](media/upgrade-2008r2-2012r2/license-terms.png)

8. Wählen **Sie Upgrade aus: Installieren Sie Windows, und halten Sie Dateien, Einstellungen** und Anwendungen für ein direktes Upgrade.

    ![Bildschirm zum Auswählen des Installations Typs](media/upgrade-2008r2-2012r2/choose-install-upgrade.png)

9. Setup erinnert Sie daran, sicherzustellen, dass Ihre apps mit Windows Server 2012 R2 kompatibel sind. verwenden Sie dazu die Informationen im Artikel [Windows Server-Installation und-Upgrade](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade) , und klicken Sie dann auf **weiter**.

    ![Bildschirm zur Überprüfung der APP-Kompatibilität](media/upgrade-2008r2-2012r2/compatibility-report.png)

10. Wenn eine Seite angezeigt wird, die Sie darüber informiert, dass das Upgrade nicht empfohlen wird, können Sie Sie ignorieren und dann **bestätigen**auswählen. Es wurde eingerichtet, um eine Neuinstallation einzugeben, aber es ist nicht erforderlich.

    ![Bildschirm mit Aktualisierungs Fortschritt](media/upgrade-2008r2-2012r2/upgrading-windows-with-progress.png)

    Das direkte Upgrade wird gestartet und zeigt den Bildschirm zum **Aktualisieren von Windows** mit dem Fortschritt an. Nachdem das Upgrade abgeschlossen ist, wird der Server neu gestartet.

## <a name="after-your-upgrade-is-done"></a>Nachdem das Upgrade abgeschlossen ist

Nachdem das Upgrade abgeschlossen ist, müssen Sie sicherstellen, dass das Upgrade auf Windows Server 2012 R2 erfolgreich war.

### <a name="to-make-sure-your-upgrade-was-successful"></a>So stellen Sie sicher, dass das Upgrade erfolgreich war

1. Öffnen Sie den Registrierungs-Editor, navigieren Sie zu HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion Hive, und zeigen Sie **ProductName**an. Sie sollten die Edition von Windows Server 2012 R2 sehen, z. b. **Windows Server 2012 R2 Datacenter**.

2. Stellen Sie sicher, dass alle Anwendungen ausgeführt werden und dass Ihre Clientverbindungen mit den Anwendungen erfolgreich sind.

Wenn Sie davon ausgehen, dass während des Upgrades ein Fehler aufgetreten ist, kopieren Sie `%SystemRoot%\Panther` das Verzeichnis `C:\Windows\Panther`(normalerweise), und wenden Sie sich an den Microsoft Support.

## <a name="next-steps"></a>Nächste Schritte

Sie können ein Upgrade von Windows Server 2012 R2 auf Windows Server 2019 durchführen. Ausführliche Anweisungen finden Sie unter [Aktualisieren von Windows Server 2012 R2 auf Windows Server 2019](upgrade-2012r2-to-2019.md).

## <a name="related-articles"></a>Verwandte Artikel

- Weitere Informationen und Informationen zu Windows Server 2012 R2 finden Sie unter [Windows Server 2012 R2 und Windows Server 2012](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh801901(v=ws.11)).
