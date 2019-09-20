---
title: Aktualisieren von Windows Server 2012 auf Windows Server 2016 | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie ein direktes Upgrade von Windows Server 2012 auf Windows Server 2016 durchführen.
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/16/2019
ms.openlocfilehash: 09c5a95e2ccd065f3ebbe551404064c39f803f2a
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/19/2019
ms.locfileid: "71124720"
---
# <a name="upgrade-windows-server-2012-to-windows-server-2016"></a>Aktualisieren von Windows Server 2012 auf Windows Server 2016

Wenn Sie dieselbe Hardware und alle Server Rollen beibehalten möchten, die Sie bereits eingerichtet haben, ohne den Server zu vereinfachen, sollten Sie ein direktes Upgrade durchführen. Ein direktes Upgrade ermöglicht es Ihnen, von einem älteren Betriebssystem zu einem neueren zu wechseln, während Ihre Einstellungen, Server Rollen und Daten unverändert bleiben. Dieser Artikel unterstützt Sie bei der Umstellung von Windows Server 2012 auf Windows Server 2016.

Verwenden Sie zum Aktualisieren auf Windows Server 2019 zunächst dieses Thema, um ein Upgrade auf Windows Server 2016 durchzuführen und dann [von Windows Server 2016 auf Windows Server 2019 zu aktualisieren](upgrade-2016-to-2019.md).

## <a name="before-you-begin-your-in-place-upgrade"></a>Bevor Sie mit dem direkten Upgrade beginnen

Bevor Sie mit dem Windows Server-Upgrade beginnen, wird empfohlen, dass Sie Informationen zu Diagnose-und Problem Behandlungszwecken von ihren Geräten sammeln. Da diese Informationen nur für die Verwendung vorgesehen sind, wenn das Upgrade fehlschlägt, müssen Sie sicherstellen, dass Sie die Informationen an einem Ort speichern, an dem Sie von Ihrem Gerät aus gelangen können.

### <a name="to-collect-your-info"></a>So erfassen Sie Ihre Informationen

1. Öffnen Sie eine Eingabeaufforderung, navigieren `c:\Windows\system32`Sie zu, und geben Sie dann **Systeminfo. exe**ein.

2. Kopieren, einfügen und speichern Sie die resultierenden Systeminformationen an einem beliebigen Speicherort Ihres Geräts.

3. Geben Sie in der Eingabeaufforderung **ipconfig/all** ein, kopieren Sie die resultierenden Konfigurationsinformationen, und fügen Sie Sie an den gleichen Speicherort wie oben ein.

4. Öffnen Sie den Registrierungs-Editor, navigieren Sie zu HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion Hive, kopieren Sie die Windows Server-Datei **BuildLabEx** (Version) und **EditionID** (Edition), und fügen Sie Sie an denselben Speicherort wie oben ein.

Nachdem Sie alle Ihre Windows Server-bezogenen Informationen gesammelt haben, empfehlen wir Ihnen dringend, Ihr Betriebssystem, Ihre apps und Ihre virtuellen Computer zu sichern. Sie müssen auch alle virtuellen Maschinen, die derzeit auf dem Server ausgeführt werden, **herunter**fahren, **schnell migrieren**oder **Live migrieren** . Während der direkten Aktualisierung können keine virtuellen Computer ausgeführt werden.

## <a name="to-perform-the-upgrade"></a>So führen Sie das Upgrade aus

1. Stellen Sie sicher, dass der **BuildLabEx** -Wert besagt, dass Sie Windows Server 2012 ausführen.

2. Suchen Sie nach den Windows Server 2016-Setup Medien, und wählen Sie dann **Setup. exe**aus.

    ![Windows-Explorer mit der Datei "Setup. exe"](media/upgrade-2012-2016/setup-2016.png)

3. Wählen Sie **Ja** aus, um den Setup Vorgang zu starten.

    ![Benutzerkontensteuerung, die die Berechtigung zum Starten des Setups anfordert](media/upgrade-2012-2016/start-setup-uac-box.png)

4. Wählen Sie auf dem Bildschirm Windows Server 2016 die Option **jetzt installieren**.

5. Wählen Sie für mit dem Internet verbundene Geräte die Option **Updates herunterladen und installieren (empfohlen)** aus.

    ![Bildschirm, der online geschaltet werden soll, um wichtige Windows-Updates zu erhalten](media/upgrade-2012-2016/imp-updates-win-setup.png)

6. Beim Setup wird die Gerätekonfiguration überprüft, Sie müssen warten, bis der Vorgang abgeschlossen ist. Wählen Sie anschließend **weiter**aus.

7. Abhängig vom Verteilungs Kanal, von dem aus Sie Windows Server-Medien (Retail, Volumenlizenz, OEM, ODM usw.) und die Lizenz für den Server erhalten haben, werden Sie möglicherweise zur Eingabe eines Lizenzschlüssels aufgefordert, um den Vorgang fortzusetzen.

    ![Bildschirm, auf dem Sie Ihre Product Key eingeben können](media/upgrade-2012-2016/enter-product-key.png)

8. Wählen Sie die Windows Server 2016-Edition aus, die Sie installieren möchten, und klicken Sie dann auf **weiter**.

    ![Bildschirm zum Auswählen der zu installierende Windows Server 2016-Edition](media/upgrade-2012-2016/select-os-edition.png)

9. Wählen Sie **akzeptieren** aus, um die Bedingungen Ihres Lizenzierungs Vertrags auf Grundlage ihres Verteilungs Kanals (z. b., Retail, Volumenlizenz, OEM, ODM usw.) zu akzeptieren.

    ![Bildschirm zur Annahme Ihres Lizenzvertrags](media/upgrade-2012-2016/license-terms.png)

10. Wählen Sie **persönliche Dateien und apps beibehalten** aus, um ein direktes Upgrade auszuführen, und klicken Sie dann auf **weiter**.

    ![Bildschirm zum Auswählen des Installations Typs](media/upgrade-2012-2016/choose-install-upgrade.png)

11. Wenn eine Seite angezeigt wird, die Sie darüber informiert, dass das Upgrade nicht empfohlen wird, können Sie Sie ignorieren und dann **bestätigen**auswählen. Es wurde eingerichtet, um eine Neuinstallation einzugeben, aber es ist nicht erforderlich.

    ![Bildschirm mit der Schaltfläche bestätigen, um sicherzustellen, dass Sie das Upgrade ausführen möchten](media/upgrade-2012-2016/confirm-upgrade-process.png)

12. Beim Setup werden Sie angewiesen, Microsoft **Endpoint Protection mithilfe der**Option "Software" zu entfernen.

    Diese Funktion ist nicht kompatibel mit Windows 10.

13. Nachdem das Gerät von Setup analysiert wurde, werden Sie aufgefordert, das Upgrade fortzusetzen, indem Sie **Installieren**auswählen.

    ![Bildschirm, auf dem angezeigt wird, dass das Upgrade gestartet werden kann](media/upgrade-2012-2016/ready-to-install.png)

    Das direkte Upgrade wird gestartet und zeigt den Bildschirm zum **Aktualisieren von Windows** mit dem Fortschritt an. Nachdem das Upgrade abgeschlossen ist, wird der Server neu gestartet.

    ![Bildschirm mit Aktualisierungs Fortschritt](media/upgrade-2012-2016/upgrading-windows-with-progress.png)

## <a name="after-your-upgrade-is-done"></a>Nachdem das Upgrade abgeschlossen ist

Nachdem das Upgrade abgeschlossen ist, müssen Sie sicherstellen, dass das Upgrade auf Windows Server 2016 erfolgreich war.

### <a name="to-make-sure-your-upgrade-was-successful"></a>So stellen Sie sicher, dass das Upgrade erfolgreich war

1. Öffnen Sie den Registrierungs-Editor, navigieren Sie zu HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion Hive, und zeigen Sie **ProductName**an. Sie sollten die Edition von Windows Server 2016 sehen, z. b. **Windows Server 2016 Datacenter**.

2. Stellen Sie sicher, dass alle Anwendungen ausgeführt werden und dass Ihre Clientverbindungen mit den Anwendungen erfolgreich sind.

Wenn Sie davon ausgehen, dass während des Upgrades ein Fehler aufgetreten ist, kopieren Sie `%SystemRoot%\Panther` das Verzeichnis `C:\Windows\Panther`(normalerweise), und wenden Sie sich an den Microsoft Support.

## <a name="next-steps"></a>Nächste Schritte

Sie können ein Upgrade von Windows Server 2016 auf Windows Server 2019 durchführen. Ausführliche Anweisungen finden Sie unter [Aktualisieren von Windows Server 2016 auf Windows Server 2019](upgrade-2016-to-2019.md).

## <a name="related-articles"></a>Verwandte Artikel

- Weitere Informationen und Informationen zu Windows Server 2016 finden Sie unter [Get Started with Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/server-basics).