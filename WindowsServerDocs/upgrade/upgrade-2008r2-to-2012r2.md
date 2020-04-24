---
title: Upgrade von Windows Server 2008 R2 auf Windows Server 2012 R2 | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie ein direktes Upgrade von Windows Server 2008 R2 auf Windows Server 2012 R2 durchführen.
ms.prod: windows-server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: 5e4436bb6e4db19e015056b67730619a93396f9e
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80854263"
---
# <a name="upgrade-windows-server-2008-r2-to-windows-server-2012-r2"></a>Upgrade von Windows Server 2008 R2 auf Windows Server 2012 R2

Wenn Sie die Hardware und alle eingerichteten Serverrollen beibehalten möchten, bietet sich ein direktes Upgrade an. Bei einem klassischen Upgrade wird von einem älteren Betriebssystem zu einem neueren gewechselt, und Ihre Einstellungen, Serverrollen und Daten bleiben erhalten. Dieser Artikel unterstützt Sie bei der Umstellung von Windows Server 2008 R2 auf Windows Server 2012 R2.

Wenn Sie ein Upgrade auf Windows Server 2019 durchführen möchten, verwenden Sie zunächst dieses Thema, um auf Windows Server 2012 R2 zu aktualisieren, und [dann ein Upgrade von Windows Server 2012 R2 auf Windows Server 2019 auszuführen](upgrade-2012r2-to-2019.md).

## <a name="before-you-begin-your-in-place-upgrade"></a>Bevor Sie mit dem direkten Upgrade beginnen

Bevor Sie mit dem Windows Server-Upgrade beginnen, wird empfohlen, dass Sie zur Diagnose und Problembehandlung Informationen von ihren Geräten sammeln. Da diese Informationen nur für den Fall eines Fehlers beim Upgrade vorgesehen sind, müssen Sie sicherstellen, dass Sie die Informationen an einem Speicherort speichern, auf den Sie ohne Ihr Gerät zugreifen können.

### <a name="to-collect-your-info"></a>So sammeln Sie Informationen

1. Öffnen Sie eine Eingabeaufforderung, navigieren Sie zu `c:\Windows\system32`, und geben Sie **systeminfo.exe** ein.

2. Die dann angezeigten Systeminformationen können Sie kopieren, einfügen und an einem Speicherort außerhalb Ihres Systems speichern.

3. Geben Sie an der Eingabeaufforderung **ipconfig /all** ein, kopieren Sie dann die angezeigten Konfigurationsinformationen, und fügen Sie sie an dem gleichen Speicherort wie oben ein.

4. Öffnen Sie den Registrierungs-Editor, wechseln Sie zum Hive „HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion“, kopieren Sie die Angaben zu Windows Server **BuildLabEx** (Version) und **EditionID** (Edition) an den gleichen Speicherort wie oben.

Nachdem Sie alle mit Windows Server zusammenhängenden Informationen gesammelt haben, raten wir dringend zu einer Sicherung Ihres Betriebssystems, Ihrer Apps und Ihrer virtuellen Computer. Ferner müssen Sie alle virtuellen Computer, die aktuell auf dem Server ausgeführt werden **herunterfahren** oder für sie eine **Schnellmigration** oder **Livemigration** ausführen. Während des direkten Upgrades können keine virtuellen Computer ausgeführt werden.

## <a name="to-perform-the-upgrade"></a>So führen Sie das Upgrade aus

1. Vergewissern Sie sich, dass der Wert von **BuildLabEx** besagt, dass Sie Windows Server 2008 R2 ausführen.

2. Suchen Sie die Windows Server 2012 R2-Setupmedien, und wählen Sie dann **setup.exe** aus.

    ![Windows-Explorer mit der Datei „setup.exe“](media/upgrade-2008r2-2012r2/setup-2012r2.png)

3. Wählen Sie **Ja** aus, um den Setupvorgang zu starten.

    ![Die Benutzerkontensteuerung bittet um die Berechtigung zum Starten des Setups](media/upgrade-2008r2-2012r2/start-setup-uac-box.png)

4. Wählen Sie auf dem Bildschirm „Windows Server 2012 R2“ **Jetzt installieren** aus.

5. Wählen Sie für Geräte mit Internetverbindung **In den Onlinemodus wechseln, um Updates jetzt zu installieren (empfohlen)** aus.

    ![Bildschirm mit der Option zum Herstellen einer Onlineverbindung zum Abrufen wichtiger Windows-Updates](media/upgrade-2008r2-2012r2/imp-updates-win-setup.png)

6. Wählen Sie die Windows Server 2012 R2-Edition aus, die Sie installieren möchten, und wählen Sie dann **Weiter** aus.

    ![Auswahlbildschirm für die zu installierende Windows Server 2012 R2-Edition](media/upgrade-2008r2-2012r2/select-os-edition.png)

7. Wählen Sie **Ich akzeptiere die Lizenzbedingungen** aus, um den Bedingungen Ihres Lizenzvertrags zuzustimmen, abhängig von Ihrem Verteilungskanal (wie etwa Einzelhandel, Volumenlizenz, OEM, ODM usw), und klicken Sie dann auf **Weiter**.

    ![Bildschirm zur Annahme Ihres Lizenzvertrags](media/upgrade-2008r2-2012r2/license-terms.png)

8. Wählen Sie **Upgrade: Windows installieren und Dateien, Einstellungen und Anwendungen behalten** aus, um ein direktes Upgrade durchzuführen.

    ![Bildschirm zur Auswahl Ihres Installationstyps](media/upgrade-2008r2-2012r2/choose-install-upgrade.png)

9. Setup fordert Sie auf, anhand der Informationen im Artikel [Windows Server: Installation und Upgrade](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade) sicherzustellen, dass Ihre Apps mit Windows Server 2012 R2 kompatibel sind, und dann **Weiter** auszuwählen.

    ![Bildschirm zur Aufforderung zur Überprüfung der App-Kompatibilität](media/upgrade-2008r2-2012r2/compatibility-report.png)

10. Wenn eine Seite angezeigt wird, die Sie informiert, dass ein Upgrade nicht empfohlen wird, können Sie sie ignorieren und **Bestätigen** auswählen. Sie wurde eingefügt, um zur Neuinstallation aufzufordern, dies ist jedoch nicht erforderlich.

    ![Bildschirm mit dem Upgradestatus](media/upgrade-2008r2-2012r2/upgrading-windows-with-progress.png)

    Das direkte Upgrade beginnt und zeigt den Bildschirm **Windows-Upgrade wird durchgeführt** mit seinem Status an. Nach dem Abschluss des Upgrades wird der Server neu gestartet.

## <a name="after-your-upgrade-is-done"></a>Nach dem Abschluss des Upgrades

Nachdem das Upgrade abgeschlossen ist, müssen Sie sich vergewissern, dass das Upgrade auf Windows Server 2012 R2 erfolgreich war.

### <a name="to-make-sure-your-upgrade-was-successful"></a>So überprüfen Sie, ob das Upgrade erfolgreich war

1. Öffnen Sie den Registrierungs-Editor, wechseln Sie zum Hive HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion, und sehen Sie sich den **ProductName** an. Sie sollten Ihre Edition von Windows Server 2012 R2 sehen, beispielsweise **Windows Server 2012 R2 Datacenter**.

2. Vergewissern Sie sich, dass alle Ihre Anwendungen ausgeführt werden, und dass Ihre Clientverbindungen mit den Anwendungen erfolgreich sind.

Wenn Sie der Ansicht sind, dass während des Upgrades ein Fehler aufgetreten ist, kopieren Sie das `%SystemRoot%\Panther`-Verzeichnis (in der Regel `C:\Windows\Panther`), und wenden Sie sich an den Microsoft Support.

## <a name="next-steps"></a>Nächste Schritte

Sie können die Umstellung von Windows Server 2012 R2 auf Windows Server 2019 mit einem oder mehreren Upgrades durchführen. Ausführliche Anweisungen finden Sie unter [Upgrade von Windows Server 2012 R2 auf Windows Server 2019](upgrade-2012r2-to-2019.md).

## <a name="related-articles"></a>Verwandte Artikel

- Weitere Details und Informationen zu Windows Server 2012 R2 finden Sie unter [Windows Server 2012 R2 und Windows Server 2012](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh801901(v=ws.11)).
