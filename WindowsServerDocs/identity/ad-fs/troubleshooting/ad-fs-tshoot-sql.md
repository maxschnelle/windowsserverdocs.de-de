---
title: AD FS-Problembehandlung – SQL-Konnektivität
description: In diesem Dokument wird beschrieben, wie verschiedene Aspekte von AD FS-Problembehandlung
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a4b7a568200bee7c2696c57f1dd964dd4e84ec21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820261"
---
# <a name="ad-fs-troubleshooting---sql-connectivity"></a>AD FS-Problembehandlung – SQL-Konnektivität
AD FS bietet die Möglichkeit, remote SQL Server für die AD FS-Farm-Daten verwenden.  Sie sehen Probleme, wenn AD FS-Servern in Ihrer Farm mit SQL Server-Back-End-Instanzen kommunizieren können.  Das folgende Dokument bietet einige grundlegende Schritte zum Testen der Kommunikation mit den Back-End-Servern.

## <a name="acquire-the-sql-database-connection-string"></a>Abrufen der Verbindungszeichenfolge der SQL-Datenbank
Zunächst muss bei der Überprüfung der SQL-Konnektivität zu testen ist, wenn AD FS über die richtigen SQL-Verbindungsinformationen verfügt.  Dies kann erfolgen mithilfe von PowerShell.

### <a name="to-acquire-the-sql-connection-string"></a>SQL-Verbindungszeichenfolge abrufen
1.  Öffnen von Windows PowerShell
2. Geben Sie Folgendes ein: `$adfs = gwmi -Namespace root/ADFS -Class SecurityTokenService` und drücken Sie EINGABETASTE
3. Geben Sie Folgendes ein: `$adfs.ConfigurationDatabaseConnectionString` und die EINGABETASTE drücken.
4. Daraufhin sollte die Verbindungszeichenfolgen-Informationen.
![](media/ad-fs-tshoot-sql/sql2.png)

## <a name="create-a-universal-data-link-udl-file-to-test-connectivity"></a>Erstellen Sie eine Datei (Universal Data Link, UDL) zum Testen der Konnektivität
Ein Universal Data Link-Datei oder der UDL-Datei ist im Grunde eine Textdatei mit der eine Datenbank-Verbindungszeichenfolge.  Mithilfe der Informationen, die, der wir oben abgerufen haben, können wir testen, und zwar unabhängig davon, ob die SQLServer auf Verbindungen reagiert.

### <a name="to-create-a-udl-file-to-test-connectivity"></a>Zum Erstellen einer Udl-Datei zum Testen der Konnektivität

1. Öffnen Sie Editor, und speichern Sie die Datei als "Test.udl".  Stellen Sie sicher, dass Sie **alle Dateien** aus der Dropdownliste für die ausgewählte **Dateityp**.
2. Doppelklicken Sie auf "Test.udl"
3. Geben Sie die folgenden Informationen: ein. **Wählen Sie aus, oder geben Sie einen Servernamen an:**  Verwenden Sie die Datenquelle die Verbindungszeichenfolge über b. **Geben Sie Informationen zum Anmelden an den Server aus:**  Verwenden Sie das AD FS-Dienstkonto oder ein Konto mit Berechtigungen für die Remoteverbindung.  Wenn das Konto ein Windows-Konto verwenden, die integrierte Authentifizierung, die andernfalls geben Sie Benutzername und Kennwort.
    c. **Wählen Sie die Datenbank auf dem Server:** Verwenden Sie den ersten Katalog aus der oben genannten Zeichenfolge.  Beispiel:  AdfsConfigurationV3.
   ![Testverbindung](media/ad-fs-tshoot-sql/sql4.png)
1. Klicken Sie auf **Testverbindung**.</br>
![Erfolg](media/ad-fs-tshoot-sql/sql3.png)

## <a name="use-sql-server-management-studio-to-test-connectivity"></a>Verwenden von SQL Server Management Studio zum Testen der Konnektivität
Sie können auch [herunterladen](https://go.microsoft.com/fwlink/?linkid=864329) und Installieren von SSMS, um die Verbindung mit der Datenbank zu testen.

###<a name="to-test-connectivity-with-ssms"></a>Zum Testen der Konnektivität mit SSMS
1. Herunterladen Sie und installieren Sie SQL Server Management Studio.
![Installieren](media/ad-fs-tshoot-sql/sql5.png)
1. Öffnen Sie SSMS, geben Sie den Namen des Servers.  Die Datenquelle von oben.
2. Verwenden Sie das AD FS-Dienstkonto oder ein Konto mit Berechtigungen für die Remoteverbindung.  Wenn das Konto ein Windows-Konto verwenden, die integrierte Authentifizierung, die andernfalls geben Sie Benutzername und Kennwort.
![Eine Verbindung herstellen](media/ad-fs-tshoot-sql/sql6.png)
1. Daraufhin sollte die linke Seite aufgefüllt.  Erweitern Sie Datenbanken aus, und stellen Sie sicher, dass Sie die AD FS-Datenbanken finden Sie unter.
![AD FS-Datenbanken](media/ad-fs-tshoot-sql/sql7.png)

## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)