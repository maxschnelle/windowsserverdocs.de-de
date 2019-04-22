> [!Note] 
> Beim Ausführen des Diagnosetools für geschützte Fabrics (Get-HgsTrace - RunDiagnostics), kann es zu der falschen Statusangabe führen, dass die HTTPS-Konfiguration fehlerhaft ist, obwohl sie nicht unterbrochen oder nicht verwendet wird. Dieser Fehler kann unabhängig von HGS-Nachweismodus zurückgegeben werden. Es gibt zahlreiche mögliche Ursachen:
>
> - HTTPS ist tatsächlich nicht ordnungsgemäß konfiguriert/beschädigt<br>
> - Sie verwenden einen admin-vertrauenswürdigen Nachweis und die Vertrauensstellung ist beschädigt<br>
> &nbsp;&nbsp;&nbsp;&nbsp;: Dies ist unabhängig davon, ob HTTPS konfiguriert ist, richtig, falsch, oder nicht in Gebrauch überhaupt.<br>
>
> Beachten Sie, dass die Diagnose nur einen falschen Status zurückgibt, wenn das Ziel ein Hyper-V-Host ist. Wenn das Ziel der Diagnose der Host Guardian Dienst ist, ist der zurückgegebene Status korrekt.

<!-- Appears in guarded-fabric-setting-up-the-host-guardian-service-hgs.md and guarded-fabric-troubleshoot-diagnostics.md
-->
