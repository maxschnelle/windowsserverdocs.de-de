---
title: Bereitstellen einer Remotedesktop-Umgebung
ms.prod: windows-server
description: Grundlegende Schritte zur Bereitstellung einer Remotedesktop-Umgebung.
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/10/2017
ms.topic: article
author: lizap
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 31bb6afaca92b36453d4565c1f79aae35a6f0900
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855753"
---
# <a name="deploy-your-remote-desktop-environment"></a>Bereitstellen einer Remotedesktop-Umgebung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Führen Sie die folgenden Schritte aus, um die Remotedesktop-Server in Ihrer Umgebung bereitzustellen. Sie können die Serverrollen auf physischen oder virtuellen Computern installieren, je nachdem, ob Sie eine lokale, cloudbasierte oder Hybrid-Umgebung erstellen. 

Wenn Sie virtuelle Computer für einen der Remotedesktopdienste-Server verwenden, stellen Sie sicher, dass Sie [diese virtuellen Computer](rds-prepare-vms.md) vorbereitet haben.
  
  
1.  Fügen Sie dem Server-Manager alle Server hinzu, die Sie für Remotedesktopdienste verwenden werden:  
    1.  Klicken Sie im Server-Manager auf **Verwalten** > **Server hinzufügen**.  
    2.  Klicken Sie auf **Jetzt suchen**.  
    3.  Klicken Sie auf die einzelnen Server in der Bereitstellung (z. B. Contoso-Cb1, Contoso-WebGw1 und Contoso-Sh1) und dann auf **OK**.  
2.  Erstellen Sie eine sitzungsbasierte Bereitstellung, um die Komponenten der Remotedesktopdienste bereitzustellen:  
    1.  Klicken Sie im Server-Manager auf **Verwalten** > **Rollen und Features hinzufügen**.  
    2.  Klicken Sie auf **Installation von Remotedesktopdiensten**, **Standardbereitstellung** und **Sitzungsbasierte Desktopbereitstellung**.  
    3.  Wählen Sie die entsprechenden Server für den RD-Verbindungsbrokerserver, den RD-Web Access-Server und den RD-Sitzungshostserver (z. B. Contoso-Cb1, Contoso-WebGw1 und Contoso-SH1) aus.  
    4.  Wählen Sie **Zielserver bei Bedarf automatisch neu starten** aus, und klicken Sie dann auf **Bereitstellen**.  
    5.  Warten Sie auf den erfolgreichen Abschluss der Bereitstellung  
3.  RD-Lizenzserver hinzufügen:  
    1.  Klicken Sie im Server-Manager auf **Remotedesktopdienste > Übersicht > +RD-Lizenzierung**.  
    2.  Wählen Sie den virtuellen Computer aus, auf dem der RD-Lizenzserver installiert werden soll (z. B. Contoso-Cb1).  
    3.  Klicken Sie auf **Weiter**, und klicken Sie dann auf **Hinzufügen**.  
4.  Aktivieren Sie den RD-Lizenzserver, und fügen Sie ihn der Gruppe „Lizenzserver“ hinzu:  
    1.  Klicken Sie im Server-Manager auf **Tools > Terminaldienste > Remotedesktoplizenzierungs-Manager**.  
    2.  Wählen Sie im RD-Lizenzierungs-Manager den Server aus, und klicken Sie dann auf **Aktion > Server aktivieren**.  
    3.  Übernehmen Sie die Standardwerte im Serveraktivierungs-Assistenten. Fahren Sie mit dem Übernehmen der Standardwerte fort, bis Sie zur Seite **Unternehmensinformationen** gelangen. Geben Sie dann die Daten zu Ihrem Unternehmen ein.  
    4.  Akzeptieren Sie die Standardwerte für die restlichen Seiten bis zur letzten Seite. Deaktivieren Sie die Option **Assistent für die Lizenzinstallation starten**, und klicken Sie dann auf **Fertig stellen**.  
    5.  Klicken Sie auf **Aktion > Konfiguration prüfen > Zu Gruppe hinzufügen > OK**. Geben Sie die Anmeldeinformationen für einen Benutzer in der Gruppe der AAD DC-Administratoren ein, und registrieren Sie ihn als SCP. Dieser Schritt funktioniert möglicherweise nicht, wenn Sie Azure AD Domain Services verwenden, aber Sie können alle Warnungen oder Fehler ignorieren.  
5.  Fügen Sie den RD-Gateway-Server und den Zertifikatsnamen hinzu:  
    1.  Klicken Sie im Server-Manager auf **Remotedesktopdienste > Übersicht > +RD-Gateway**.  
    2.  Wählen Sie im Assistenten „RD-Gatewayserver hinzufügen“ den virtuellen Computer aus, auf dem Sie den RD-Gateway-Server installieren möchten (z. B. Contoso-WebGw1).  
    3.  Geben Sie den SSL-Zertifikatsnamen für den RD-Gateway-Server unter Verwendung des externen vollqualifizierten DNS-Namens (FQDN) des RD-Gateway-Servers ein. In Azure ist dies die Bezeichnung **DNS-Name**, die das Format „servicename.location.cloudapp.azure.com“ verwendet. Beispiel: contoso.westus.cloudapp.azure.com.  
    4.  Klicken Sie auf **Weiter**, und klicken Sie dann auf **Hinzufügen**.
6.  Erstellen und installieren Sie selbstsignierte Zertifikate für die RD-Gateway- und RD-Verbindungsbroker-Server.

       > [!NOTE]
       > Wenn Sie Zertifikate von einer vertrauenswürdigen Zertifizierungsstelle bereitstellen und installieren, führen Sie die Verfahren von Schritt h bis Schritt k für die einzelnen Rollen aus. Für jedes dieser Zertifikate muss die PFX-Datei verfügbar sein.
       
    1.  Klicken Sie im Server-Manager auf **Remotedesktopdienste > Übersicht > Aufgaben > Bereitstellungseigenschaften bearbeiten**.  
    2.  Erweitern Sie **Zertifikate**, und scrollen Sie dann nach unten zur Tabelle. Klicken Sie auf **RD-Gateway > Neues Zertifikat erstellen**.  
    3.  Geben Sie den Zertifikatsnamen über den externen FQDN des RD-Gatewayservers (z. B. contoso.westus.cloudapp.azure.com) und anschließend das Kennwort ein.  
    4.  Wählen Sie **Dieses Zertifikat speichern** aus, und navigieren Sie dann zu dem freigegebenen Ordner, den Sie in einem vorherigen Schritt für Zertifikate erstellt haben. (Beispiel: \Contoso-Cb1\Certificates.)  
    5.  Geben Sie einen Dateinamen für das Zertifikat ein (z. B. ContosoRdGwCert), und klicken Sie dann auf **Speichern**.  
    6.  Wählen Sie **Hinzufügen des Zertifikats zum Zertifikatsspeicher der vertrauenswürdigen Stammzertifizierungsstellen auf den Zielcomputern zulassen** aus, und klicken Sie dann auf **OK**.  
    7.  Klicken Sie auf **Übernehmen**, und warten Sie dann, bis das Zertifikat erfolgreich auf den RD-Gateway-Server angewendet wurde.  
    8.  Klicken Sie auf **RD-Web Access > Vorhandenes Zertifikat auswählen**.  
    9.  Navigieren Sie zu dem Zertifikat, das für den RD-Gateway-Server erstellt wurde (z. B. ContosoRdGwCert), und klicken Sie dann auf **Öffnen**.  
    10. Geben Sie das Kennwort für das Zertifikat ein, wählen Sie **Hinzufügen des Zertifikats zum Speicher für vertrauenswürdige Stammzertifikate auf den Zielcomputern zulassen** aus, und klicken Sie dann auf **OK**.  
    11. Klicken Sie auf **Übernehmen**, und warten Sie dann, bis das Zertifikat erfolgreich auf den RD-Web Access-Server angewendet wurde.  
    12. Wiederholen Sie die Teilschritte 1-11 für den **RD-Verbindungsbroker – Einmaliges Anmelden aktivieren** und **RD-Verbindungsbroker – Veröffentlichungsdienste** unter Verwendung des internen FQDN des RD-Verbindungsbroker-Servers für den Namen des neuen Zertifikats (z. B. Contoso-Cb1.Contoso.com).  
7.  Exportieren Sie selbstsignierte öffentliche Zertifikate, und kopieren Sie sie auf einen Clientcomputer. Wenn Sie Zertifikate von einer vertrauenswürdigen Zertifizierungsstelle verwenden, können Sie diesen Schritt überspringen.  
    1.  Starten Sie „certlm.msc“.  
    2.  Erweitern Sie **Persönlich**, und klicken Sie auf **Zertifikate**.  
    3.  Klicken Sie im rechten Bereich mit der rechten Maustaste auf das RD-Verbindungsbroker-Zertifikat, das für die Clientauthentifizierung vorgesehen ist, z. B. **Contoso-Cb1.Contoso.com**.  
    4.  Klicken Sie auf **Alle Aufgaben > Exportieren**.  
    5.  Übernehmen Sie die Standardoptionen im Assistenten für den Zertifikatsexport, bis Sie die Seite **Zu exportierende Datei** erreichen.  
    6.  Navigieren Sie zu dem freigegebenen Ordner, den Sie für Zertifikate erstellt haben, z. B. „\Contoso-Cb1\Certificates“.  
    7.  Geben Sie einen Dateinamen ein, z. B. ContosoCbClientCert, und klicken Sie dann auf **Speichern**.  
    8.  Klicken Sie auf **Weiter**und dann auf **Fertig stellen**.  
    9.  Wiederholen Sie die Teilschritte 1-8 für das RD-Gateway- und -Web-Zertifikat (z. B. contoso.westus.cloudapp.azure.com), und geben Sie dem exportierten Zertifikat einen entsprechenden Dateinamen, z. B. **ContosoWebGwClientCert**.  
    10. Navigieren Sie im Datei-Explorer zu dem Ordner, in dem die Zertifikate gespeichert sind, z. B. „\Contoso-Cb1\Certificates“.  
    11. Wählen Sie die beiden exportierten Clientzertifikate aus, klicken Sie dann mit der rechten Maustaste darauf und klicken Sie auf **Kopieren**.  
    12. Fügen Sie die Zertifikate auf dem lokalen Clientcomputer ein.  
8.  Konfigurieren Sie die Bereitstellungseigenschaften für RD-Gateway und RD-Lizenzierung:  
    1.  Klicken Sie im Server-Manager auf **Remotedesktopdienste > Übersicht > Aufgaben > Bereitstellungseigenschaften bearbeiten**.  
    2.  Erweitern Sie **RD-Gateway**, und deaktivieren Sie die Option **RD-Gatewayserver für lokale Adressen umgehen**.  
    3.  Erweitern Sie **RD-Lizenzierung**, und wählen Sie **Pro Benutzer** aus.  
    4.  Klicken Sie auf **OK**.  
10. Erstellen Sie eine Sitzungssammlung. Diese Schritte erstellen eine einfache Sammlung. Weitere Informationen zu Sammlungen finden Sie unter [Erstellen einer Remotedesktopdienste-Sammlung zum Ausführen von Desktops und Apps](rds-create-collection.md).
 
    1.  Klicken Sie im Server-Manager auf **Remotedesktopdienste > Sammlungen > Tasks > Sitzungssammlungen erstellen**.  
    2.  Geben Sie einen Sammlungsnamen ein (z. B. ContosoDesktop).  
    3.  Wählen Sie einen RD-Sitzungshostserver (Contoso-Sh1) aus, übernehmen Sie die Standardbenutzergruppen (Contoso\Domain Users), und geben Sie den UNC-Pfad (Universal Naming Convention) zu den oben erstellten Benutzerprofil-Datenträgern ein (\Contoso-Cb1\UserDisks).  
    4.  Legen Sie eine maximale Größe fest, und klicken Sie dann auf **Erstellen**.  
  

Sie haben jetzt eine grundlegende Infrastruktur für Remotedesktopdienste erstellt. Wenn Sie eine Bereitstellung mit Hochverfügbarkeit erstellen müssen, können Sie einen [Verbindungsbrokercluster](rds-connection-broker-cluster.md) oder einen [zweiten RD-Sitzungshostserver](rds-scale-rdsh-farm.md) hinzufügen.

