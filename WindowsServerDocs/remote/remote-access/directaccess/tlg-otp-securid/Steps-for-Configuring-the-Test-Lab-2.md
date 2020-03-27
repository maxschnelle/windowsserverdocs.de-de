---
title: Schritte zum Konfigurieren der Testumgebung
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a40183c-afd1-43ca-b306-05745640a37d
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d7acc592bcec4d43972da73a782b0894847ddb13
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308534"
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
  


