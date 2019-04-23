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
ms.openlocfilehash: acfdd99fa67e218f58fe650de5607f2a5ba97bf8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833831"
---
# <a name="deploy-your-remote-desktop-environment"></a>Bereitstellen einer Remotedesktop-Umgebung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Verwenden Sie die folgenden Schritte aus, um die Remotedesktop-Server in Ihrer Umgebung bereitstellen. Sie können die Serverrollen auf physischen oder virtuellen Computern, je nachdem, ob Sie einer lokalen, cloudbasierten erstellen oder Hybrid-Umgebung installieren. 

Wenn Sie virtuelle Computer für einen beliebigen Server Remote Desktop Services verwenden, stellen Sie sicher, dass [diese virtuellen Computer vorbereitet](rds-prepare-vms.md).
  
  
1.  Fügen Sie allen Servern, die Sie verwenden, für die Remote Desktop Services Server-Manager möchten:  
    1.  Klicken Sie in Server-Manager auf **verwalten > Hinzufügen von Servern**.  
    2.  Klicken Sie auf **Jetzt suchen**.  
    3.  Klicken Sie auf jedem Server in der Bereitstellung (z. B. Contoso-Cb1, Contoso-WebGw1 und Contoso-Sh1), und klicken Sie auf **OK**.  
2.  Erstellen Sie eine sitzungsbasierte Bereitstellung zum Bereitstellen von Remote Desktop Services-Komponenten:  
    1.  Klicken Sie im Server-Manager **verwalten > Rollen und Features hinzufügen**.  
    2.  Klicken Sie auf **Remote Desktop Services-Installation**, **Standardbereitstellung**, und **sitzungsbasierte desktopbereitstellung**.  
    3.  Wählen Sie die entsprechenden Server für den Remotedesktop-Verbindungsbrokerserver, Web Access für Remotedesktop-Server und Remotedesktop-Sitzungshostserver (z. B. Contoso-Cb1, Contoso-WebGw1, und Contoso-SH1, bzw.).  
    4.  Wählen Sie **automatisch neu starten die Zielserver bei Bedarf**, und klicken Sie dann auf **bereitstellen**.  
    5.  Warten Sie, bis die Bereitstellung erfolgreich abgeschlossen.  
3.  Fügen Sie die Remotedesktop-Lizenzserver hinzu:  
    1.  Klicken Sie im Server-Manager **Remote Desktop Services > Übersicht > + RD-Lizenzierung**.  
    2.  Wählen Sie den virtuellen Computer, in denen der Remotedesktop-Lizenzserver (z. B. Contoso-Cb1) installiert werden soll.  
    3.  Klicken Sie auf **Weiter**, und klicken Sie dann auf **hinzufügen**.  
4.  Aktivieren Sie den Remotedesktop-Lizenzserver, und der Lizenzserver-Gruppe hinzufügen:  
    1.  Klicken Sie im Server-Manager **Tools > "Terminal Services" > Remotedesktoplizenzierungs-Manager**.  
    2.  Remotedesktoplizenzierungs-Manager, wählen Sie den Server, und klicken Sie dann auf **Aktion > Server aktivieren**.  
    3.  Akzeptieren Sie die Standardwerte in der Serveraktivierungs-Assistent, um Standardwerte zu übernehmen, bis Sie erreichen die **Unternehmensinformationen** Seite. Geben Sie dann die Informationen für Ihr Unternehmen.  
    4.  Übernehmen Sie die Standardwerte für die verbleibenden Seiten, bis die letzte Seite. Klare **starten Lizenzinstallations-Assistenten jetzt**, und klicken Sie dann auf **Fertig stellen**.  
    5.  Klicken Sie auf **Aktion > Überprüfen Sie die Konfiguration > zu Gruppe hinzufügen > OK**. Geben Sie Anmeldeinformationen für einen Benutzer in der Administratorengruppe und als Dienstverbindungspunkt registrieren. Dieser Schritt funktioniert möglicherweise nicht, wenn Sie Azure AD Domain Services verwenden, aber Sie können alle Warnungen oder Fehler ignorieren.  
5.  Fügen Sie den Remotedesktopgateway-Server und das Zertifikat-Namen:  
    1.  Klicken Sie im Server-Manager **Remote Desktop Services > Übersicht > + RD-Gateway**.  
    2.  Wählen Sie den virtuellen Computer, in dem Sie den RD-Gateway-Server (z. B. Contoso-WebGw1) installieren möchten, im Assistenten RD-Gateway-Server hinzufügen.  
    3.  Geben Sie den Namen des SSL-Zertifikat für den RD-Gateway-Server mit den externen vollqualifizierten DNS-Namen (FQDN) des RD-Gatewayservers ein. In Azure, ist dies die **DNS-Namen** Bezeichnung und den servicename.location.cloudapp.azure.com Format verwendet. Z. B. contoso.westus.cloudapp.azure.com.  
    4.  Klicken Sie auf **Weiter**, und klicken Sie dann auf **hinzufügen**.
6.  Erstellen Sie und installieren Sie selbstsignierte Zertifikate für die RD-Gateway und RD Connection Broker Server.

       > [!NOTE]
       > Wenn Sie bereitstellen und Installieren von Zertifikaten von einer vertrauenswürdigen Zertifizierungsstelle verwenden, können führen Sie die Prozeduren aus Schritt h k für jede Rolle schrittweise aus. Sie benötigen, um die PFX-Datei verfügbar für jede dieser Zertifikate zu erhalten.
       
    1.  Im Server-Manager, klicken Sie auf **Remote Desktop Services > Übersicht > Vorgänge > bearbeiten Eigenschaften**.  
    2.  Erweitern Sie **Zertifikate**, und klicken Sie dann die Tabelle scrollen. Klicken Sie auf **RD-Gateway > Neues Zertifikat erstellen**.  
    3.  Geben Sie den Zertifikatnamen, mit der externe FQDN des Remotedesktop-Gatewayservers (z. B. contoso.westus.cloudapp.azure.com), und geben Sie dann das Kennwort.  
    4.  Wählen Sie **Store dieses Zertifikat** und navigieren Sie dann auf den freigegebenen Ordner, die Sie für die Zertifikate in einem vorherigen Schritt erstellt haben. (Z. B. \Contoso-Cb1\Certificates.)  
    5.  Geben Sie einen Dateinamen für das Zertifikat (z. B. ContosoRdGwCert), und klicken Sie dann auf **speichern**.  
    6.  Wählen Sie **können Sie das Zertifikat dem Zertifikatspeicher "Vertrauenswürdige Stammzertifizierungsstellen" auf den Zielcomputern hinzugefügt werden**, und klicken Sie dann auf **OK**.  
    7.  Klicken Sie auf **übernehmen**, und warten Sie, bis das Zertifikat auf dem Remotedesktop-Gatewayserver wurde erfolgreich angewendet werden.  
    8.  Klicken Sie auf **Web Access für Remotedesktop > Option Vorhandenes Zertifikat**.  
    9.  Navigieren Sie zu dem Zertifikat für den RD-Gateway-Server (z. B. ContosoRdGwCert) erstellt, und klicken Sie dann auf **öffnen**.  
    10. Geben Sie das Kennwort für das Zertifikat, wählen **können Sie das Zertifikat hinzugefügt werden in den vertrauenswürdigen Stamm-Zertifikatspeicher auf den Zielcomputern**, und klicken Sie dann auf **OK**.  
    11. Klicken Sie auf **übernehmen**, und warten Sie, bis das Zertifikat wurde erfolgreich auf dem Web Access für Remotedesktop-Server angewendet werden.  
    12. Wiederholen Sie die Schritte 1 bis 11 für den **RD-Verbindungsbroker - einmaliges Anmelden aktivieren** und **RD-Verbindungsbroker - Publishingdienste**, verwenden den internen FQDN des Remotedesktop-Verbindungsbrokerservers für die neue Name des Zertifikats (z. B. Contoso-Cb1.Contoso.com).  
7.  Exportieren Sie des selbstsignierten öffentlichen Zertifikate, und kopieren Sie sie auf einen Clientcomputer. Wenn Sie Zertifikate von einer vertrauenswürdigen Zertifizierungsstelle verwenden, können Sie diesen Schritt überspringen.  
    1.  Starten Sie "certlm.msc".  
    2.  Erweitern Sie **persönliche**, und klicken Sie dann auf **Zertifikate**.  
    3.  Im rechten Bereich mit der Maustaste des RD Connection Broker-Zertifikats zur Clientauthentifizierung, z. B. **Contoso-Cb1.Contoso.com**.  
    4.  Klicken Sie auf **alle Aufgaben > Exportieren**.  
    5.  Akzeptieren Sie die Standardoptionen im Zertifikatexport-Assistenten übernehmen die Standardwerte, bis Sie erreichen die **zu exportierende Datei** Seite.  
    6.  Navigieren Sie zu den freigegebenen Ordner für Zertifikate, z. B. \Contoso-Cb1\Certificates erstellten.  
    7.  Geben Sie einen Dateinamen ein, z. B. ContosoCbClientCert, und klicken Sie dann auf **speichern**.  
    8.  Klicken Sie auf **Weiter**und dann auf **Fertig stellen**.  
    9.  Wiederholen Sie die Teilschritte 1 bis 8 für das RD-Gateway und Web-Zertifikat (z. B. contoso.westus.cloudapp.azure.com), sodass dem exportierten Zertifikat Dateiname eignet, z. B. **ContosoWebGwClientCert**.  
    10. Navigieren Sie im Datei-Explorer zu dem Ordner, in denen die Zertifikate gespeichert werden, z. B. \Contoso-Cb1\Certificates.  
    11. Wählen Sie die zwei exportierte Clientzertifikate, und klicken Sie dann mit der rechten Maustaste sie und klicken Sie auf **Kopie**.  
    12. Fügen Sie den Zertifikaten auf dem lokalen Clientcomputer aus.  
8.  Konfigurieren Sie die Bereitstellungseigenschaften RD-Gateway und RD-Lizenzierung:  
    1.  Im Server-Manager, klicken Sie auf **Remote Desktop Services > Übersicht > Vorgänge > bearbeiten Eigenschaften**.  
    2.  Erweitern Sie **RD-Gateway** und deaktivieren Sie die **Remotedesktop-Gatewayserver für lokale Adressen umgehen** Option.  
    3.  Erweitern Sie **RD-Lizenzierung** , und wählen Sie **pro Benutzer**  
    4.  Klicken Sie auf **OK**.  
10. Erstellen einer sitzungssammlung. Diesen Schritten erstellen eine basic-Auflistung. Sehen Sie sich [erstellen Sie eine Remote Desktop Services-Sammlung für Desktops und apps ausführen](rds-create-collection.md) für Weitere Informationen zu Sammlungen.
 
    1.  Klicken Sie im Server-Manager **Remote Desktop Services > Sammlungen > Vorgänge > Sitzungssammlung erstellen**.  
    2.  Geben Sie eine Auflistung von Namen (z. B. ContosoDesktop) aus.  
    3.  Wählen Sie ein Remotedesktop-Sitzungshostserver (Contoso-Sh1), akzeptieren Sie die Standard-Benutzergruppen (namens-Benutzer), und geben Sie den Pfad für die Universal Naming Convention (UNC) die Benutzerprofil-Datenträger oben (\Contoso-Cb1\UserDisks) erstellt haben.  
    4.  Legen Sie eine Maximalgröße, und klicken Sie dann auf **erstellen**.  
  

Sie haben nun eine grundlegende Remote Desktop Services-Infrastruktur erstellt. Wenn Sie eine hoch verfügbare Bereitstellung erstellen möchten, können Sie Hinzufügen einer [Connection Broker Cluster](rds-connection-broker-cluster.md) oder [zweiten Remotedesktop-Sitzungshostserver](rds-scale-rdsh-farm.md).

