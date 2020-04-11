---
title: Upgrade von Windows Server 2012 R2 auf Windows Server 2019 | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie ein direktes Upgrade von Windows Server 2012 R2 auf Windows Server 2019 durchführen.
ms.prod: windows-server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: 02d6dd21b798346245f209174902b6f4fdf24ff8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853343"
---
# <a name="upgrade-windows-server-2012-r2-to-windows-server-2019"></a>Upgrade von Windows Server 2012 R2 auf Windows Server 2019

Wenn Sie die Hardware und alle eingerichteten Serverrollen beibehalten möchten, bietet sich ein direktes Upgrade an. Bei einem klassischen Upgrade wird von einem älteren Betriebssystem zu einem neueren gewechselt, und Ihre Einstellungen, Serverrollen und Daten bleiben erhalten. Dieser Artikel unterstützt Sie bei der Umstellung von Windows Server 2012 R2 auf Windows Server 2019.

## <a name="before-you-begin-your-in-place-upgrade"></a>Bevor Sie mit dem direkten Upgrade beginnen

Bevor Sie mit dem Windows Server-Upgrade beginnen, wird empfohlen, dass Sie zur Diagnose und Problembehandlung Informationen von ihren Geräten sammeln. Da diese Informationen nur für den Fall eines Fehlers beim Upgrade vorgesehen sind, müssen Sie sicherstellen, dass Sie die Informationen an einem Speicherort speichern, auf den Sie ohne Ihr Gerät zugreifen können.

### <a name="to-collect-your-info"></a>So sammeln Sie Informationen

1. Öffnen Sie eine Eingabeaufforderung, navigieren Sie zu `c:\Windows\system32`, und geben Sie **systeminfo.exe** ein.

2. Die dann angezeigten Systeminformationen können Sie kopieren, einfügen und an einem Speicherort außerhalb Ihres Systems speichern.

3. Geben Sie an der Eingabeaufforderung **ipconfig /all** ein, kopieren Sie dann die angezeigten Konfigurationsinformationen, und fügen Sie sie an dem gleichen Speicherort wie oben ein.

4. Öffnen Sie den Registrierungs-Editor, wechseln Sie zum Hive „HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion“, kopieren Sie die Angaben zu Windows Server **BuildLabEx** (Version) und **EditionID** (Edition) an den gleichen Speicherort wie oben.

Nachdem Sie alle mit Windows Server zusammenhängenden Informationen gesammelt haben, raten wir dringend zu einer Sicherung Ihres Betriebssystems, Ihrer Apps und Ihrer virtuellen Computer. Ferner müssen Sie alle virtuellen Computer, die aktuell auf dem Server ausgeführt werden **herunterfahren** oder für sie eine **Schnellmigration** oder **Livemigration** ausführen. Während des direkten Upgrades können keine virtuellen Computer ausgeführt werden.

## <a name="to-perform-the-upgrade"></a>So führen Sie das Upgrade aus

1. Vergewissern Sie sich, dass der Wert von **BuildLabEx** besagt, dass Sie Windows Server 2012 R2 ausführen.

2. Suchen Sie die Windows Server 2019-Setupmedien, und wählen Sie dann **setup.exe** aus.

    ![Windows-Explorer mit der Datei „setup.exe“](media/upgrade-2012r2-2019/setup-2019.png)

3. Wählen Sie **Ja** aus, um den Setupvorgang zu starten.

    ![Die Benutzerkontensteuerung bittet um die Berechtigung zum Starten des Setups](media/upgrade-2012r2-2019/start-setup-uac-box.png)

4. Wählen Sie für Geräte mit Internetverbindung die Option **Updates, Treiber und optionale Features herunterladen (empfohlen)** und dann **Weiter** aus.

    ![Bildschirm mit der Option zum Herstellen einer Onlineverbindung zum Abrufen wichtiger Windows-Updates](media/upgrade-2012r2-2019/online-updates-win-setup.png)

5. Setup überprüft Ihre Gerätekonfiguration; warten Sie bis zum Abschluss der Überprüfung, und wählen Sie dann **Weiter** aus.

6. Je nach dem Verteilungskanal, über den Sie Ihre Windows Server-Medien erhalten haben (Einzelhandel, Volumenlizenz, OEM, ODM usw.), und der Lizenz für den Server, werden Sie möglicherweise aufgefordert, einen Lizenzschlüssel einzugeben, bevor Sie fortfahren können.

7. Wählen Sie die Windows Server 2019-Edition aus, die Sie installieren möchten, und wählen Sie dann **Weiter** aus.

    ![Auswahlbildschirm für die zu installierende Windows Server 2012 R2-Edition](media/upgrade-2012r2-2019/select-os-edition.png)

8. Wählen Sie **Ich stimme zu** aus, um den Bedingungen Ihres Lizenzvertrags zuzustimmen, abhängig von Ihrem Verteilungskanal (wie etwa Einzelhandel, Volumenlizenz, OEM, ODM usw).

    ![Bildschirm zur Annahme Ihres Lizenzvertrags](media/upgrade-2012r2-2019/license-terms.png)

9. Setup empfiehlt Ihnen, Microsoft Endpoint Protection mithilfe von **Programme hinzufügen/entfernen** zu entfernen.

    Diese Funktion ist nicht mit Windows Server 2019 kompatibel.

10. Wählen Sie **Persönliche Dateien und Apps beibehalten** aus, um ein direktes Upgrade festzulegen, und wählen Sie dann **Weiter** aus.

    ![Bildschirm zur Auswahl Ihres Installationstyps](media/upgrade-2012r2-2019/choose-install-upgrade.png)

11. Nachdem Setup Ihr Gerät analysiert hat, werden Sie aufgefordert, den Upgradevorgang fortzusetzen, indem Sie **Installieren** auswählen.

    ![Bildschirm, der anzeigt, dass Sie zum Starten des Upgrades bereit sind](media/upgrade-2012r2-2019/ready-to-install.png)

    Das direkte Upgrade beginnt und zeigt den Bildschirm **Windows-Upgrade wird durchgeführt** mit seinem Status an. Nach dem Abschluss des Upgrades wird der Server neu gestartet.

    ![Bildschirm mit dem Upgradestatus](media/upgrade-2012r2-2019/upgrading-windows-with-progress.png)

## <a name="after-your-upgrade-is-done"></a>Nach dem Abschluss des Upgrades

Nachdem das Upgrade abgeschlossen ist, müssen Sie sich vergewissern, dass das Upgrade auf Windows Server 2019 erfolgreich war.

### <a name="to-make-sure-your-upgrade-was-successful"></a>So überprüfen Sie, ob das Upgrade erfolgreich war

1. Öffnen Sie den Registrierungs-Editor, wechseln Sie zum Hive HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion, und sehen Sie sich den **ProductName** an. Sie sollten Ihre Edition von Windows Server 2019 sehen, beispielsweise **Windows Server 2019 Datacenter**.

2. Vergewissern Sie sich, dass alle Ihre Anwendungen ausgeführt werden, und dass Ihre Clientverbindungen mit den Anwendungen erfolgreich sind.

Wenn Sie der Ansicht sind, dass während des Upgrades ein Fehler aufgetreten ist, kopieren Sie das `%SystemRoot%\Panther`-Verzeichnis (in der Regel `C:\Windows\Panther`), und wenden Sie sich an den Microsoft Support.

## <a name="related-articles"></a>Verwandte Artikel

- Weitere Details und Informationen zu Windows Server 2019 finden Sie unter [Erste Schritte mit Windows Server 2019](https://docs.microsoft.com/windows-server/get-started-19/get-started-19).