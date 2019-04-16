---
title: Bereitstellen einer Remotedesktop-Umgebung
ms.custom: na
ms.prod: windows-server-threshold
description: Grundlegende Schritte zum Bereitstellen einer Remotedesktop-Umgebung.
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/10/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: a5a56d56038d94869c5246f8d4d3eae2796616a3
ms.sourcegitcommit: d3f73936160505a40633ad8dd5931ac5fe3eccdb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297439"
---
# Bereitstellen einer Remotedesktop-Umgebung

>Gilt für: WindowsServer (Semi-Annual Channel), WindowsServer 2019, WindowsServer 2016

Verwenden Sie die folgenden Schritte aus, um den Remotedesktop-Servern in Ihrer Umgebung bereitstellen. Sie können die Serverrollen auf physischen oder virtuellen Computern, je nachdem, ob Sie eine lokale, Cloud-basierte, erstellen oder hybridumgebung installieren. 

Wenn Sie virtuelle Computer für alle Server Remote Desktop Services verwenden, stellen Sie sicher, dass Sie [Diese virtuellen Computer vorbereitet](rds-prepare-vms.md)haben.
  
  
1.  Fügen Sie alle Server, die Sie vorhaben, für Remote Desktop Services zum Server-Manager verwenden:  
    1.  Im Server-Manager, klicken Sie auf **Verwalten > Server hinzufügen**.  
    2.  Klicken Sie auf **Jetzt suchen**.  
    3.  Klicken Sie auf jedem Server in der Bereitstellung (z. B. Contoso-Cb1 Contoso-WebGw1 und Contoso-Sh1), und klicken Sie auf **OK**.  
2.  Erstellen Sie eine Sitzung-basierte Bereitstellung zum Bereitstellen von Remotedesktopdienste-Komponenten:  
    1.  Klicken Sie im Server-Manager auf **Verwalten > Rollen und Features hinzufügen**.  
    2.  Klicken Sie auf **Remote Desktop Services-Installation**, **Standard-Bereitstellung**und **Sitzung-basierten desktop-Bereitstellung**.  
    3.  Wählen Sie die entsprechenden Server für den Remotedesktop-Verbindungsbrokerserver Web Access für Remotedesktop-Server und Remotedesktop-Sitzungshostserver (z. B. Contoso-Cb1, Contoso-WebGw1, und Contoso-SH1, bzw.).  
    4.  Wählen Sie **den Zielserver neu starten, automatisch, wenn erforderlich**, und klicken Sie dann auf **Bereitstellen**.  
    5.  Warten Sie, bis die Bereitstellung erfolgreich abgeschlossen  
3.  Fügen Sie RD-Lizenzserver hinzu:  
    1.  Klicken Sie im Server-Manager auf **Remote Desktop Services > Übersicht > + RD-Lizenzierung**.  
    2.  Wählen Sie den virtuellen Computer, auf der Lizenzserver RD (z. B. Contoso-Cb1) installiert wird.  
    3.  Klicken Sie auf **Weiter**, und klicken Sie auf **Hinzufügen**.  
4.  Aktivieren des Lizenzservers RD und die Lizenzserver-Gruppe hinzugefügt:  
    1.  Klicken Sie im Server-Manager auf **Tools > Terminaldienste > Lizenzierung-Manager**.  
    2.  Wählen Sie in RD-Lizenzierung-Manager den Server und klicken Sie dann auf **Aktion > Server aktivieren**.  
    3.  Akzeptieren Sie die Standardwerte im Assistenten Standardwerte akzeptieren, bis Sie die Seite **Unternehmensinformationen** erreichen. Geben Sie Informationen zu Ihrem Unternehmen an.  
    4.  Übernehmen Sie die Standardwerte für die verbleibenden Seiten, bis der letzten Seite. Deaktivieren Sie **Installieren Lizenzen Assistent für starten**, und klicken Sie dann auf **Fertig stellen**.  
    5.  Klicken Sie auf die **Aktion > Konfiguration prüfen > hinzu Gruppe > OK**. Geben Sie Anmeldeinformationen für einen Benutzer in der Gruppe AAD DC Administratoren und als SCP registrieren. Dieser Schritt funktioniert möglicherweise nicht, wenn Sie Azure Active Directory Domain Services verwenden, aber Sie können alle Warnungen oder Fehler ignorieren.  
5.  Fügen Sie der RD-Gateway-Server und Zertifikat Name:  
    1.  Klicken Sie im Server-Manager auf **Remote Desktop Services > Übersicht > + RD-Gateway**.  
    2.  Wählen Sie im Assistenten für die RD-Gateway-Server Hinzufügen der virtuelle Computer, wo Sie den RD-Gateway-Server (z. B. Contoso-WebGw1) installieren möchten.  
    3.  Geben Sie den Namen des SSL-Zertifikat für den RD-Gateway-Server mit den externen vollständig qualifizierten DNS-Namen (FQDN) des Servers RD-Gateway ein. In Azure Dies ist die Bezeichnung für die **DNS-Namen** und das Format servicename.location.cloudapp.azure.com verwendet. Beispielsweise contoso.westus.cloudapp.azure.com.  
    4.  Klicken Sie auf **Weiter**, und klicken Sie auf **Hinzufügen**.
6.  Erstellen Sie und installieren Sie selbstsignierte Zertifikate für die RD-Gateway und RD Connection Broker-Server.

       > [!NOTE]
       > Wenn Sie bereitstellen und Installieren von Zertifikaten von einer vertrauenswürdigen Zertifizierungsstelle, führen Sie die Verfahren aus Schritt h Schritt k für jede Rolle. Sie müssen die verfügbaren PFX-Datei für jede dieser Zertifikate verfügen.
       
    1.  Klicken Sie im Server-Manager auf **Remote Desktop Services > Übersicht > Aufgaben > Bereitstellungseigenschaften bearbeiten**.  
    2.  Erweitern Sie **Zertifikate**, und Sie dann einen Bildlauf in der Tabelle. Klicken Sie auf **RD-Gateway > erstellen Neues Zertifikat**.  
    3.  Geben Sie den Zertifikatnamen, die mit den externen FQDN des RD-Gateway-Servers (z. B. contoso.westus.cloudapp.azure.com), und geben Sie dann das Kennwort.  
    4.  **Store dieses Zertifikat** auswählen, und klicken Sie dann auf den freigegebenen Ordner für Zertifikate in einem vorherigen Schritt erstellten navigieren. (Z. B. \Contoso Cb1\Certificates.)  
    5.  Geben Sie einen Namen für das Zertifikat (z. B. ContosoRdGwCert), und klicken Sie dann auf **Speichern**.  
    6.  Wählen Sie **das Zertifikat im Zertifikatspeicher "Vertrauenswürdige Stammzertifizierungsstellen" auf den Zielcomputern hinzugefügt werden zulassen**, und klicken Sie dann auf **OK**.  
    7.  Klicken Sie auf **Übernehmen**, und warten Sie für das Zertifikat an den Server RD-Gateway erfolgreich angewendet werden.  
    8.  Klicken Sie auf **Web Access für Remotedesktop > vorhandenes Zertifikat auswählen**.  
    9.  Navigieren Sie zu verwendende Zertifikat, das für den RD-Gateway-Server (z. B. ContosoRdGwCert) erstellt, und klicken Sie dann auf **Öffnen**.  
    10. Geben Sie das Kennwort für das Zertifikat ein, wählen **ermöglichen das Zertifikat hinzugefügt werden an den Store vertrauenswürdige Stammzertifikat auf den Zielcomputern**, und klicken Sie dann auf **OK**.  
    11. Klicken Sie auf **Übernehmen**, und warten Sie auf das Zertifikat mit dem Web Access für Remotedesktop-Server erfolgreich angewendet werden.  
    12. Wiederholen Sie die Schritte 1 bis 11 für die **RD Connection Broker - einmaliges Anmelden aktivieren** und **RD Connection Broker - Veröffentlichen von Diensten**, mit der interne FQDN des RD Connection Broker-Servers für das neue Zertifikat Namen (z. B. Contoso-Cb1.Contoso.com).  
7.  Exportieren Sie selbstsignierte öffentliche Zertifikate, und kopieren Sie sie auf einem Clientcomputer installieren. Wenn Sie Zertifikate von einer vertrauenswürdigen Zertifizierungsstelle verwenden, können Sie diesen Schritt überspringen.  
    1.  Starten Sie certlm.msc.  
    2.  Erweitern Sie **Eigene**, und klicken Sie dann auf **Zertifikate**.  
    3.  Im rechten Bereich mit der rechten Maustaste des RD Connection Broker-Zertifikats für die Clientauthentifizierung, z. B. **Contoso-Cb1.Contoso.com**vorgesehen.  
    4.  Klicken Sie auf **Alle Aufgaben > exportieren**.  
    5.  Akzeptieren Sie, dass die Standardoptionen im der Zertifikatexport-Assistent Standardwerte zu übernehmen, bis die **Exportdatei** Seite.  
    6.  Navigieren Sie zu den freigegebenen Ordner, die, den Sie für Zertifikate, z. B. \Contoso-Cb1\Certificates erstellt.  
    7.  Geben Sie einen Dateinamen, z. B. ContosoCbClientCert, und klicken Sie dann auf **Speichern**.  
    8.  Klicken Sie auf **Weiter**, und klicken Sie dann auf **Fertig stellen**.  
    9.  Wiederholen Sie die Schritte 1 bis 8 für den RD-Gateway und Web-Zertifikat, (z. B. contoso.westus.cloudapp.azure.com), für dem exportierten Zertifikat einen entsprechenden Dateinamen ein, z. B. **ContosoWebGwClientCert**.  
    10. Navigieren Sie im Datei-Explorer zu dem Ordner, in denen die Zertifikate gespeichert sind, z. B. \Contoso-Cb1\Certificates.  
    11. Wählen Sie die zwei exportierten Clientzertifikate, und klicken Sie dann mit der rechten Maustaste darauf, und klicken Sie auf **Kopieren**.  
    12. Fügen Sie die Certifcates auf dem lokalen Client-Computer.  
8.  Konfigurieren Sie die Bereitstellungseigenschaften Remotedesktopgateway und RD-Lizenzierung:  
    1.  Klicken Sie im Server-Manager auf **Remote Desktop Services > Übersicht > Aufgaben > Bereitstellungseigenschaften bearbeiten**.  
    2.  Erweitern Sie **RD-Gateway** , und deaktivieren Sie die Option **Remotedesktop-Gatewayserver für lokale Adressen umgehen** .  
    3.  Erweitern Sie **RD-Lizenzierung** und wählen Sie **Pro Benutzer**  
    4.  Klicken Sie auf **OK**.  
10. Erstellen Sie eine Sitzung-Sammlung. Folgendermaßen erstellen Sie eine grundlegende Sammlung. Sehen Sie sich [Erstellen einer Remotedesktopdienste-Sammlung für Desktops und apps ausgeführt](rds-create-collection.md) , Weitere Informationen zu Sammlungen.
 
    1.  Klicken Sie im Server-Manager auf **Remote Desktop Services > Sammlungen > Aufgaben > erstellen Sitzung Sammlung**.  
    2.  Geben Sie eine Sammlung Namen (z. B. ContosoDesktop).  
    3.  Wählen Sie einen RD-Sitzungshostserver (Contoso-Sh1), akzeptieren Sie die Standard-Benutzergruppen (namens Benutzer), und geben Sie den Pfad Universal Naming Convention (UNC) auf die Benutzerprofil Laufwerke oben (\Contoso-Cb1\UserDisks) erstellt.  
    4.  Legen Sie eine Maximalgröße, und klicken Sie auf **Erstellen**.  
  

Sie haben nun eine grundlegende Remotedesktopdienste-Infrastruktur erstellt. Wenn Sie eine hoch verfügbare Bereitstellung erstellen müssen, können Sie eine [Connection Broker Cluster](rds-connection-broker-cluster.md) oder einem [zweiten RD-Sitzungshostserver](rds-scale-rdsh-farm.md)hinzufügen.

