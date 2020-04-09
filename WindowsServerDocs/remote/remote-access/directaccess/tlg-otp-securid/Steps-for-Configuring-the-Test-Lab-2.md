---
title: Schritte zum Konfigurieren der Testumgebung
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 0a40183c-afd1-43ca-b306-05745640a37d
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fc40bf8f1b4bcb3d28b23abd981575a6438f871e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814383"
---
# <a name="steps-for-configuring-the-test-lab"></a>Schritte zum Konfigurieren der Testumgebung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In den folgenden Schritten wird beschrieben, wie Sie die Remote Zugriffs Infrastruktur konfigurieren, den RAS-Server und-Client konfigurieren und die DirectAccess-Konnektivität aus den Subnetzen homenet und Internet testen.  
  
In dieser Test Umgebungs Anleitung erstellen Sie einen Remote Zugriff mit OTP-Umgebung, indem Sie die folgenden Schritte ausführen:  
  
-   [Schritt 1: vervollständigen Sie die DirectAccess-Konfiguration](assetId:///4dbf877f-02fb-439b-907a-f5b3f1d8afa6). Führen Sie alle Schritte in der [Test Umgebungs Anleitung zum Veranschaulichen der Einrichtung von DirectAccess Single Server mit gemischtem IPv4 und IPv6](https://go.microsoft.com/fwlink/p/?LinkId=237004)aus.  
  
-   [Schritt 2: Konfigurieren von App1](assetId:///c1bb590f-91d4-4ed5-bceb-b0e36eabd4ff). Konfigurieren Sie App1 mit OTP-Zertifikat Vorlagen für die Verwendung durch Edge1.  
  
-   [Schritt 3: Konfigurieren von DC1](assetId:///904a6edc-a771-45ed-9630-a34a680bb522). Überprüfen Sie den in DC1 definierten Benutzer Prinzipal Namen.  
  
-   [Schritt 7: Installieren und Konfigurieren von RSA](assetId:///baa4c28c-add7-42e2-8afd-ccc7a559406a) Installieren und konfigurieren Sie RSA, einen RADIUS-und einen OTP-Server, und konfigurieren Sie Edge1 für OTP.  
  
-   [Schritt 11: Überprüfen der OTP-Integrität auf Edge1](assetId:///3b397a4a-8478-47f2-a932-9e8e048c14ba) Stellen Sie sicher, dass der Status von OTP auf dem RAS-Server fehlerfrei ist.  
  
-   [Schritt 8: Testen der DirectAccess-Konnektivität aus dem homenet-Subnetz](assetId:///ba1652a6-0692-4add-91ca-34a84956ba14) Testen Sie die Funktion von DirectAccess OTP hinter einem NAT-Gerät.  
  
-   [Schritt 10: Testen der DirectAccess-Konnektivität über das Internet](assetId:///321149eb-5f23-4a0b-b8fb-1244540126e9). Testen Sie die DirectAccess-Client Konnektivität über das Internet.  
  
-   [Schritt 12: Erstellen einer Momentaufnahme der Konfiguration](assetId:///8a51ed3c-9c32-402f-85d1-617ce46845b4) Nachdem Sie die Testumgebung abgeschlossen haben, erstellen Sie eine Momentaufnahme der funktionierenden DirectAccess-Konfiguration mit OTP-Konfiguration, damit Sie später zu dieser zurückkehren können, um weitere Szenarios zu testen.  
  


