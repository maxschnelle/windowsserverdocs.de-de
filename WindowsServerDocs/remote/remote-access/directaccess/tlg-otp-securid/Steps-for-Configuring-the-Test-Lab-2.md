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
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ef5ce37983b8565fab8287eeaae7423be0c269f6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404728"
---
# <a name="steps-for-configuring-the-test-lab"></a>Schritte zum Konfigurieren der Testumgebung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In den folgenden Schritten wird beschrieben, wie Sie die Remote Zugriffs Infrastruktur konfigurieren, den RAS-Server und-Client konfigurieren und die DirectAccess-Konnektivität aus den Subnetzen homenet und Internet testen.  
  
In dieser Test Umgebungs Anleitung erstellen Sie einen Remote Zugriff mit OTP-Umgebung, indem Sie die folgenden Schritte ausführen:  
  
-   [SCHRITT 1: Vervollständigen Sie die DirectAccess-Konfiguration @ no__t-0. Führen Sie alle Schritte in der Test Umgebungs Anleitung für [aus: Veranschaulichen der Einrichtung eines einzelnen Servers für DirectAccess mit gemischtem IPv4 und IPv6 @ no__t-0.  
  
-   [SCHRITT 2: Konfigurieren Sie App1 @ no__t-0. Konfigurieren Sie App1 mit OTP-Zertifikat Vorlagen für die Verwendung durch Edge1.  
  
-   [SCHRITT 3: Konfigurieren Sie DC1 @ no__t-0. Überprüfen Sie den in DC1 definierten Benutzer Prinzipal Namen.  
  
-   [SCHRITT 7: Installieren und konfigurieren Sie RSA @ no__t-0. Installieren und konfigurieren Sie RSA, einen RADIUS-und einen OTP-Server, und konfigurieren Sie Edge1 für OTP.  
  
-   [SCHRITT 11: Überprüfen Sie die OTP-Integrität auf Edge1 @ no__t-0. Stellen Sie sicher, dass der Status von OTP auf dem RAS-Server fehlerfrei ist.  
  
-   [SCHRITT 8: Testen Sie die DirectAccess-Konnektivität aus dem homenet-Subnetz @ no__t-0. Testen Sie die Funktion von DirectAccess OTP hinter einem NAT-Gerät.  
  
-   [SCHRITT 10: Testen Sie die DirectAccess-Konnektivität über das Internet @ no__t-0. Testen Sie die DirectAccess-Client Konnektivität über das Internet.  
  
-   [SCHRITT 12: Momentaufnahme der Konfiguration @ no__t-0. Nachdem Sie die Testumgebung abgeschlossen haben, erstellen Sie eine Momentaufnahme der funktionierenden DirectAccess-Konfiguration mit OTP-Konfiguration, damit Sie später zu dieser zurückkehren können, um weitere Szenarios zu testen.  
  


