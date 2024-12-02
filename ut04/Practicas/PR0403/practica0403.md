# EL PIPELINE EN POWERSHELL
## Práctica 0403

### 1. El comando Get-Date muestra la fecha y hora actual. Mostrar por pantalla únicamente el año en que estamos
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0403> Get-Date | Get-Member 
PS C:\GIT\aso_abgg\ut04\Practicas\PR0403> Get-Date | Select-Object -Property Year

Year
----
2024
```
```powershell
PS C:\GIT\aso_abgg\ut04\Practicas\PR0403> Get-Date | Select-Object  Year         

Year
----
2024
```
### 2. Mostrar por pantalla, en formato tabla, las propiedades TpmPresent, TpmReady, TpmEnabled y TpmActivated del comando Get-TPM
```powershell
PS C:\Users\Alumno> Get-TPM | Select-Object -Property TpmPresent, TpmReady, TpmEnabled, TpmActivated | Format-Table -AutoSize

TpmPresent TpmReady TpmEnabled TpmActivated
---------- -------- ---------- ------------
      True     True       True         True

```
## En los ejercicios siguientes se trabajará con los ficheros devueltos por el comando Get-ChildItem C:\Windows\System32
### 1. Mostrar por pantalla el número de ficheros y directorios que hay en ese directorio
```powershell
PS C:\Windows\System32> (Get-ChildItem).count
4754
```
```powershell
PS C:\Windows\System32> Get-ChildItem | Measure-Object


Count    : 4754
Average  :
Sum      :
Maximum  :
Minimum  :
Property :
```
 
### 2. Los objetos devueltos por el comando anterior tienen una propiedad denominada Extensión. Calcular el número de ficheros en el directorio que tienen la extensión .dll
```powershell
PS C:\Windows\System32> Get-ChildItem | Where-Object Name -like *.dll | Measure-Object


Count    : 3515
Average  :
Sum      :
Maximum  :
Minimum  :
Property :
```
```powershell
PS C:\Windows\System32> (Get-ChildItem | Where-Object Name -like *.dll).count
3515
```
### 3. Mostrar los ficheros del directorio con extensión  .exe que tengan un tamaño superior a 50000 bytes
```powershell
PS C:\Windows\System32> Get-ChildItem | Where-Object Name -like *.exe | Where-Object Length -gt 50000


    Directorio: C:\Windows\System32


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        17/09/2024      9:42        1175552 AgentService.exe
-a----        17/09/2024      9:41         307200 AggregatorHost.exe
-a----        17/09/2024      9:41        3249768 aitstatic.exe
-a----        07/05/2022      7:19         110592 alg.exe
-a----        13/06/2023      8:41         600048 amdfendrsr.exe
-a----        20/05/2024     22:15         470952 amdlogum.exe
-a----        20/05/2024     22:16       11526264 amdsmi.exe
-a----        17/09/2024      9:41         143360 AppHostRegistrationVerifier.exe
-a----        17/09/2024      9:41          77824 appidcertstorecheck.exe
-a----        17/09/2024      9:41         155648 appidpolicyconverter.exe
-a----        17/09/2024      9:41          62968 AppInstallerBackgroundUpdate.exe
-a----        17/09/2024      9:41          96456 ApplicationFrameHost.exe
-a----        17/09/2024      9:42        1118208 ApplySettingsTemplateCatalog.exe
-a----        17/09/2024      9:41        1203976 ApplyTrustOffline.exe
-a----        17/09/2024      9:40         253952 ApproveChildRequest.exe
-a----        17/09/2024      9:42         771480 AppVClient.exe
-a----        17/09/2024      9:42         189920 AppVDllSurrogate.exe
-a----        17/09/2024      9:42         181752 AppVNice.exe
-a----        17/09/2024      9:42         226784 AppVShNotify.exe
-a----        17/09/2024      9:42         131072 AssignedAccessGuard.exe
-a----        17/09/2024      9:41         139264 AtBroker.exe
-a----        20/05/2024     22:17         535672 atieah64.exe
-a----        20/05/2024     22:17         998416 atieclxx.exe
-a----        17/09/2024      9:40         935360 audiodg.exe
-a----        07/05/2022      7:20          57344 auditpol.exe
-a----        07/05/2022      7:19         158400 AuthHost.exe
-a----        22/12/2023     13:30        1052672 autochk.exe
-a----        17/04/2024     11:59          81920 AxInstUI.exe
-a----        07/05/2022     12:28         131072 baaupdate.exe
-a----        07/05/2022      7:19          61440 BackgroundTransferHost.exe
-a----        17/09/2024      9:40         266240 bcdboot.exe
-a----        17/09/2024      9:40         501128 bcdedit.exe
-a----        17/09/2024      9:42         409600 bdechangepin.exe
-a----        07/05/2022     12:28         151552 BdeHdCfg.exe
-a----        22/12/2023     13:31          77824 BdeUISrv.exe
-a----        07/05/2022     12:28         319552 bdeunlock.exe
-a----        17/09/2024      9:41         666696 BioIso.exe
-a----        07/05/2022     12:28         184320 BitLockerDeviceEncryption.exe
-a----        22/12/2023     13:31         122880 BitLockerWizard.exe
-a----        22/12/2023     13:31         122880 BitLockerWizardElev.exe
-a----        07/05/2022      7:19         237568 bitsadmin.exe
-a----        07/05/2022      7:19         107872 bootsect.exe
-a----        17/09/2024      9:41         155648 browserexport.exe
-a----        17/09/2024      9:41          66944 browser_broker.exe
-a----        22/12/2023     13:30          65536 bthudtask.exe
-a----        17/09/2024      9:41         110592 ByteCodeGenerator.exe
-a----        07/05/2022      7:20          57344 cacls.exe
-a----        07/05/2022     12:28          59240 CameraSettingsUIHost.exe
-a----        07/05/2022      7:20          92304 CastSrv.exe
-a----        17/09/2024      9:41          65536 CertEnrollCtrl.exe
-a----        22/12/2023     13:31         491520 certreq.exe
-a----        17/09/2024      9:42        1536000 certutil.exe
-a----        17/09/2024      9:41         125488 changepk.exe
-a----        17/09/2024      9:41         217088 charmap.exe
-a----        22/12/2023     13:31          53248 CheckNetIsolation.exe
-a----        07/05/2022      7:20          53248 choice.exe
-a----        07/05/2022      7:20          61440 CIDiag.exe
-a----        07/05/2022      7:19          73728 cipher.exe
-a----        17/09/2024      9:40         316784 CiTool.exe
-a----        17/09/2024      9:41         299008 cleanmgr.exe
-a----        20/05/2024     22:15         360872 clinfo.exe
-a----        07/05/2022      7:20          53248 clip.exe
-a----        17/09/2024      9:40         241664 ClipDLS.exe
-a----        17/09/2024      9:40         234864 ClipRenew.exe
-a----        17/09/2024      9:41        1133736 ClipUp.exe
-a----        17/09/2024      9:41          95600 CloudExperienceHostBroker.exe
-a----        17/09/2024      9:41         108960 CloudNotifications.exe
-a----        17/09/2024      9:41         323584 cmd.exe
-a----        07/05/2022      7:19          73728 cmdl32.exe
-a----        07/05/2022      7:19          65536 cmmon32.exe
-a----        07/05/2022      7:19         122880 cmstp.exe
-a----        07/05/2022      7:19         106496 colorcpl.exe
-a----        07/05/2022      7:19          69632 compact.exe
-a----        17/09/2024      9:41         308744 CompatTelRunner.exe
-a----        22/12/2023     13:31         114688 CompMgmtLauncher.exe
-a----        17/04/2024     11:59         147456 CompPkgSrv.exe
-a----        17/09/2024      9:41          69632 ComputerDefaults.exe
-a----        17/09/2024      9:41        1040384 conhost.exe
-a----        17/09/2024      9:41         226784 consent.exe
-a----        07/05/2022      7:19         135168 control.exe
-a----        17/09/2024      9:41         238960 convertvhd.exe
-a----        17/09/2024      9:41          77824 coredpussvr.exe
-a----        17/09/2024      9:41         431272 CredentialEnrollmentManager.exe
-a----        17/09/2024      9:41         187360 CredentialUIBroker.exe
-a----        17/09/2024      9:42         102400 credwiz.exe
-a----        17/09/2024      9:41         192512 cscript.exe
-a----        07/05/2022      7:20         114688 cttune.exe
-a----        07/05/2022      7:20          65536 cttunesvr.exe
-a----        17/09/2024      9:41         672312 curl.exe
-a----        17/09/2024      9:41         159744 CustomInstallExec.exe
-a----        17/09/2024      9:42        1462272 CustomShellHost.exe
-a----        17/09/2024      9:41         151552 dasHost.exe
-a----        17/09/2024      9:41         304512 DataExchangeHost.exe
-a----        17/09/2024      9:41         188416 DataStoreCacheDumpTool.exe
-a----        07/05/2022      7:19         122880 dccw.exe
-a----        07/05/2022      7:19          69632 ddodiag.exe
-a----        07/05/2022      7:20         245760 Defrag.exe
-a----        07/05/2022      7:19          57344 deploymentcsphelper.exe
-a----        17/09/2024      9:41         155648 desktopimgdownldr.exe
-a----        22/12/2023     13:30         161136 DeviceCensus.exe
-a----        17/09/2024      9:41         118784 DeviceCredentialDeployment.exe
-a----        17/09/2024      9:41         528384 DeviceEnroller.exe
-a----        17/09/2024      9:41         118784 DevicePairingWizard.exe
-a----        07/05/2022      7:20         110592 DeviceProperties.exe
-a----        07/05/2022      7:20          73728 DFDWiz.exe
-a----        07/05/2022      7:20         139264 dfrgui.exe
-a----        20/05/2024     22:16         543248 dgtrayicon.exe
-a----        07/05/2022      7:20          57344 dialer.exe
-a----        17/09/2024      9:41         176128 directxdatabaseupdater.exe
-a----        07/05/2022      7:19         180224 diskpart.exe
-a----        07/05/2022      7:19         368640 diskraid.exe
-a----        07/05/2022      7:19          94208 DiskSnapshot.exe
-a----        22/12/2023     13:31          69632 diskusage.exe
-a----        22/12/2023     13:30         337392 Dism.exe
-a----        22/12/2023     13:30         139264 dispdiag.exe
-a----        17/04/2024     11:59        1877472 DisplaySwitch.exe
-a----        07/05/2022      7:19         102400 djoin.exe
-a----        17/09/2024      9:41         204800 dmcertinst.exe
-a----        07/05/2022      7:19          61440 dmcfghost.exe
-a----        17/09/2024      9:41         163840 dmclient.exe
-a----        07/05/2022      7:19          53248 DmNotificationBroker.exe
-a----        17/09/2024      9:41          57344 DmOmaCpMo.exe
-a----        07/05/2022      7:19          57344 dnscacheugc.exe
-a----        07/05/2022      7:19          98304 dpapimig.exe
-a----        07/05/2022      7:20          98304 DpiScaling.exe
-a----        07/05/2022      7:19         102400 driverquery.exe
-a----        17/09/2024      9:41         380928 drvinst.exe
-a----        22/12/2023     13:30          53248 DsmUserTask.exe
-a----        17/09/2024      9:41         458752 dsregcmd.exe
-a----        17/09/2024      9:41         155648 dtdump.exe
-a----        17/09/2024      9:41          94208 dusmtask.exe
-a----        17/09/2024      9:41         118784 dwm.exe
-a----        17/09/2024      9:41         258048 DWWIN.EXE
-a----        07/05/2022      7:19         270336 dxdiag.exe
-a----        17/09/2024      9:41         135168 dxgiadaptercache.exe
-a----        17/09/2024      9:41         327680 Dxpserver.exe
-a----        17/09/2024      9:41         364544 EaseOfAccessDialog.exe
-a----        07/05/2022      7:20          96448 easinvoker.exe
-a----        17/09/2024      9:42          94208 EASPolicyManagerBrokerHost.exe
-a----        17/09/2024      9:41         167936 EDPCleanup.exe
-a----        17/09/2024      9:41          90112 edpnotify.exe
-a----        17/09/2024      9:42         122880 EduPrintProv.exe
-a----        20/05/2024     22:17         502392 EEURestart.exe
-a----        07/05/2022      7:20         147456 EhStorAuthn.exe
-a----        17/09/2024      9:41         180224 EoAExperiences.exe
-a----        17/09/2024      9:41         483328 esentutl.exe
-a----        07/05/2022      7:20          58736 esimtool.exe
-a----        17/09/2024      9:41         380928 eudcedit.exe
-a----        07/05/2022      7:20          65536 eventcreate.exe
-a----        07/05/2022      7:20         106496 eventvwr.exe
-a----        07/05/2022      7:19          69632 expand.exe
-a----        07/05/2022      7:19          57344 extrac32.exe
-a----        17/09/2024      9:42         464336 fclip.exe
-a----        22/12/2023     13:31         159744 fhmanagew.exe
-a----        17/09/2024      9:41         151552 FileDialogBroker.exe
-a----        22/12/2023     13:31         262144 FileHistory.exe
-a----        07/05/2022      7:20          61440 findstr.exe
-a----        17/09/2024      9:42         102400 fodhelper.exe
-a----        17/09/2024      9:42         135168 Fondue.exe
-a----        17/09/2024      9:41         856848 fontdrvhost.exe
-a----        17/09/2024      9:41         147456 fontview.exe
-a----        07/05/2022      7:20          69632 forfiles.exe
-a----        17/09/2024      9:42         133792 FsIso.exe
-a----        17/09/2024      9:41         167936 fsquirt.exe
-a----        17/09/2024      9:41         271840 fsutil.exe
-a----        17/04/2024     11:59          73728 ftp.exe
-a----        17/09/2024      9:42         212992 fvenotify.exe
-a----        07/05/2022     12:28         188416 fveprompt.exe
-a----        17/09/2024      9:42         290816 FXSCOVER.exe
-a----        17/09/2024      9:42         712704 FXSSVC.exe
-a----        17/09/2024      9:42          73728 FXSUNATD.exe
-a----        17/09/2024      9:41         376832 GameBarPresenceWriter.exe
-a----        17/09/2024      9:41          75368 GameInputSvc.exe
-a----        17/09/2024      9:41        1339392 GamePanel.exe
-a----        22/12/2023     13:30         666672 GenValObj.exe
-a----        07/05/2022      7:19         102400 getmac.exe
-a----        17/09/2024      9:41         294912 gpresult.exe
-a----        07/05/2022     12:28          65536 gpscript.exe
-a----        17/04/2024     11:59          53248 gpupdate.exe
-a----        07/05/2022      7:19          77824 hdwwiz.exe
-a----        27/06/2024     13:10         681440 HotkeyServiceDSU.exe
-a----        17/09/2024      9:41        1783280 hvax64.exe
-a----        17/09/2024      9:41        1967608 hvix64.exe
-a----        17/09/2024      9:42         194016 hvsievaluator.exe
-a----        07/05/2022      7:20          57344 icacls.exe
-a----        17/09/2024      9:40          61440 IcsEntitlementHost.exe
-a----        17/09/2024      9:41         282624 ie4uinit.exe
-a----        17/09/2024      9:41         122880 ie4ushowIE.exe
-a----        17/09/2024      9:41         491520 IESettingSync.exe
-a----        17/09/2024      9:41          98304 ieUnatt.exe
-a----        07/05/2022      7:20         184320 iexpress.exe
-a----        17/09/2024      9:41         147456 immersivetpmvscmgrsvr.exe
-a----        17/09/2024      9:41         131072 InputSwitchToastHandler.exe
-a----        17/09/2024      9:42         165360 iotstartup.exe
-a----        17/04/2024     11:59          53248 ipconfig.exe
-a----        17/09/2024      9:41          69632 iscsicli.exe
-a----        17/09/2024      9:41          57344 ISM.exe
-a----        17/09/2024      9:41         143360 isoburn.exe
-a----        07/05/2022      7:20          61440 klist.exe
-a----        07/05/2022      7:20          61440 ksetup.exe
-a----        17/09/2024      9:41          77824 LanguageComponentsInstallerComHandler.exe
-a----        17/09/2024      9:41          86016 LaunchWinApp.exe
-a----        17/09/2024      9:41         229376 LegacyNetUXHost.exe
-a----        17/09/2024      9:41          73728 LicenseManagerShellext.exe
-a----        17/09/2024      9:41         532480 licensingdiag.exe
-a----        07/05/2022      7:19         174928 LicensingUI.exe
-a----        17/09/2024      9:41         176128 LiveCaptions.exe
-a----        17/09/2024      9:42         102400 LocationNotificationWindows.exe
-a----        17/09/2024      9:41         104840 LockAppHost.exe
-a----        07/05/2022      7:19          71656 LockScreenContentServer.exe
-a----        07/05/2022      7:19          77824 lodctr.exe
-a----        07/05/2022     12:28         131072 logagent.exe
-a----        07/05/2022      7:20         118784 logman.exe
-a----        07/05/2022      7:19          61440 lpkinstall.exe
-a----        17/09/2024      9:41         765952 lpksetup.exe
-a----        17/09/2024      9:41         106496 lpremove.exe
-a----        17/09/2024      9:41         356800 LsaIso.exe
-a----        17/04/2024     11:59          84096 lsass.exe
-a----        17/09/2024      9:41         749568 Magnify.exe
-a----        07/05/2022      7:19         106496 makecab.exe
-a----        07/05/2022     12:28         262144 manage-bde.exe
-a----        17/09/2024      9:42         198112 mavinject.exe
-a----        17/09/2024      9:42         843776 mblctr.exe
-a----        17/09/2024      9:41         335872 MBR2GPT.EXE
-a----        07/05/2022      7:19         126976 mcbuilder.exe
-a----        17/09/2024      9:42         487424 MDEServer.exe
-a----        17/09/2024      9:40         172032 MDMAgent.exe
-a----        17/09/2024      9:41         192512 MDMAppInstaller.exe
-a----        17/09/2024      9:41          90112 MdmDiagnosticsTool.exe
-a----        07/05/2022      7:20         106496 MdRes.exe
-a----        07/05/2022      7:20         110592 MdSched.exe
-a----        17/04/2024     12:00          71784 mfpmp.exe
-a----        17/09/2024      9:42         417792 Microsoft.Uev.CscUnpinTool.exe
-a----        17/09/2024      9:42          83456 Microsoft.Uev.SyncController.exe
-a----        17/09/2024      9:40         122880 MicrosoftEdgeBCHost.exe
-a----        17/09/2024      9:41         122880 MicrosoftEdgeCP.exe
-a----        17/09/2024      9:40         122880 MicrosoftEdgeDevTools.exe
-a----        17/09/2024      9:41          81920 MicrosoftEdgeSH.exe
-a----        17/09/2024      9:42        1949696 mmc.exe
-a----        17/09/2024      9:41        1482752 mmgaserver.exe
-a----        17/09/2024      9:42         131072 mobsync.exe
-a----        17/09/2024      9:41          81920 MoNotificationUxStub.exe
------        15/04/2024      9:04         918944 MpSigStub.exe
-a----        16/09/2024      9:29      199688632 MRT.exe
-a----        07/05/2022      7:19         102400 MSchedExe.exe
-a----        17/09/2024      9:42         262144 msconfig.exe
-a----        17/09/2024      9:42         581632 msdt.exe
-a----        17/09/2024      9:41         204800 msdtc.exe
-a----        17/09/2024      9:42         176128 msiexec.exe
-a----        17/09/2024      9:42         389120 msinfo32.exe
-a----        17/09/2024      9:42         614400 msra.exe
-a----        07/05/2022      7:19          98304 MsSpellCheckingHost.exe
-a----        17/09/2024      9:42        1388544 mstsc.exe
-a----        07/05/2022      7:19         159744 mtstocom.exe
-a----        17/09/2024      9:41         114688 MuiUnattend.exe
-a----        07/05/2022      7:20          77824 MultiDigiMon.exe
-a----        17/09/2024      9:41         630784 Narrator.exe
-a----        22/12/2023     13:30          90112 ndadmin.exe
-a----        07/05/2022      7:20          54616 NDKPerfCmd.exe
-a----        07/05/2022      7:20          50528 NDKPing.exe
-a----        07/05/2022      7:20          81920 net.exe
-a----        22/12/2023     13:31         204800 net1.exe
-a----        07/05/2022      7:19          65536 netcfg.exe
-a----        17/09/2024      9:41          98304 NetCfgNotifyObjectHost.exe
-a----        22/12/2023     13:31          53248 NetEvtFwdr.exe
-a----        07/05/2022      7:19          53248 netiougc.exe
-a----        17/09/2024      9:41          65536 Netplwiz.exe
-a----        07/05/2022      7:20         118784 netsh.exe
-a----        17/09/2024      9:41          61440 NETSTAT.EXE
-a----        22/12/2023     13:30          90112 newdev.exe
-a----        17/09/2024      9:41         642040 NgcIso.exe
-a----        17/09/2024      9:42         577536 nltest.exe
-a----        17/09/2024      9:42         360448 notepad.exe
-a----        07/05/2022      7:19         102400 nslookup.exe
-a----        17/09/2024      9:42       11212272 ntkrla57.exe
-a----        17/09/2024      9:41       12064224 ntoskrnl.exe
-a----        17/09/2024      9:41          86016 ntprint.exe
-a----        07/05/2022      7:20          98304 odbcad32.exe
-a----        07/05/2022      7:19          98304 ofdeploy.exe
-a----        17/09/2024      9:41         479232 omadmclient.exe
-a----        17/09/2024      9:41         139264 omadmprc.exe
-a----        07/05/2022     12:28       50312608 OneDriveSetup.exe
-a----        17/09/2024      9:41         125392 OOBE-Maintenance.exe
-a----        07/05/2022      7:20          90112 openfiles.exe
-a----        17/09/2024      9:41         158560 OpenWith.exe
-a----        17/09/2024      9:42         135168 OptionalFeatures.exe
-a----        17/09/2024      9:41         569344 osk.exe
-a----        17/09/2024      9:41          65536 PackagedCWALauncher.exe
-a----        07/05/2022     12:28         102400 PackageInspector.exe
-a----        17/09/2024      9:41          67640 PasswordOnWakeSettingFlyout.exe
-a----        17/09/2024      9:41         118784 pcalua.exe
-a----        17/09/2024      9:41         212992 pcaui.exe
-a----        17/09/2024      9:42         180224 perfmon.exe
-a----        07/05/2022      7:19         129504 phoneactivate.exe
-a----        17/09/2024      9:41         162568 PickerHost.exe
-a----        17/09/2024      9:40         143360 PinEnrollmentBroker.exe
-a----        17/09/2024      9:41         274432 PkgMgr.exe
-a----        17/09/2024      9:42         697824 PktMon.exe
-a----        07/05/2022      7:19          73728 PnPUnattend.exe
-a----        17/04/2024     11:59         204800 pnputil.exe
-a----        29/08/2024      6:57         565248 poqexec.exe
-a----        19/10/2012      6:52        3867040 PortChanger.exe
-a----        17/09/2024      9:41          69632 pospaymentsworker.exe
-a----        17/09/2024      9:41         118784 powercfg.exe
-a----        07/05/2022      7:20         278528 PresentationHost.exe
-a----        17/09/2024      9:42         258048 PresentationSettings.exe
-a----        17/09/2024      9:41          53248 prevhost.exe
-a----        07/05/2022     12:28          94208 PrintBrmUi.exe
-a----        22/12/2023     13:30         634880 printfilterpipelinesvc.exe
-a----        07/05/2022      7:19          94208 PrintIsolationHost.exe
-a----        22/12/2023     13:30          81920 printui.exe
-a----        17/09/2024      9:41          69632 proquota.exe
-a----        17/09/2024      9:42          81920 provlaunch.exe
-a----        17/09/2024      9:41         114688 provtool.exe
-a----        17/09/2024      9:42         290680 ProximityUxHost.exe
-a----        17/09/2024      9:42         413696 psr.exe
-a----        07/05/2022      7:20          53248 pwlauncher.exe
-a----        08/11/2019     10:15        3600896 pwNative.exe
-a----        17/09/2024      9:42         159744 raserver.exe
-a----        07/05/2022      7:19          57344 rasphone.exe
-a----        17/09/2024      9:42         585728 rdpclip.exe
-a----        17/09/2024      9:42         501104 rdpinit.exe
-a----        17/09/2024      9:42         212992 rdpinput.exe
-a----        07/05/2022      7:20          81920 RdpSa.exe
-a----        07/05/2022      7:20          61440 RdpSaProxy.exe
-a----        07/05/2022      7:20          57344 RdpSaUacHelper.exe
-a----        17/09/2024      9:42         751072 rdpshell.exe
-a----        22/12/2023     13:31         118784 rdpsign.exe
-a----        07/05/2022      7:19          73728 rdrleakdiag.exe
-a----        17/09/2024      9:41          86016 readCloudDataSettings.exe
-a----        22/12/2023     13:30          69632 ReAgentc.exe
-a----        07/05/2022      7:20         212992 recdisc.exe
-a----        07/05/2022      7:20         307200 RecoveryDrive.exe
-a----        17/09/2024      9:41        1757184 refsutil.exe
-a----        07/05/2022      7:20         102400 reg.exe
-a----        07/05/2022      7:20          65536 regini.exe
-a----        07/05/2022      7:19         147456 rekeywiz.exe
-a----        07/05/2022      7:20          73728 relog.exe
-a----        17/09/2024      9:41         212992 RelPost.exe
-a----        17/09/2024      9:42         118784 RemoteAppLifetimeManager.exe
-a----        17/09/2024      9:42         151552 repair-bde.exe
-a----        17/09/2024      9:42         131072 resmon.exe
-a----        22/12/2023     13:30         602112 RMActivate.exe
-a----        22/12/2023     13:30         626688 RMActivate_isv.exe
-a----        22/12/2023     13:30         520192 RMActivate_ssp.exe
-a----        22/12/2023     13:30         524288 RMActivate_ssp_isv.exe
-a----        17/09/2024      9:41         143360 rmttpmvscmgrsvr.exe
-a----        17/09/2024      9:41         180224 Robocopy.exe
-a----        07/05/2022      7:19          53248 RpcPing.exe
-a----        07/05/2022     12:28          77824 rrinstaller.exe
-a----        17/09/2024      9:42         294912 rstrui.exe
-a----        17/09/2024      9:41          90112 rundll32.exe
-a----        17/09/2024      9:41          98304 runexehelper.exe
-a----        17/09/2024      9:41         114688 runonce.exe
-a----        17/09/2024      9:41         133656 RuntimeBroker.exe
-a----        07/05/2022      7:20          98304 sc.exe
-a----        07/05/2022      7:19         258048 schtasks.exe
-a----        17/09/2024      9:41         212992 sdbinst.exe
-a----        17/09/2024      9:42          98304 sdchange.exe
-a----        22/12/2023     13:30        1110016 sdclt.exe
-a----        17/09/2024      9:42          57344 sdiagnhost.exe
-a----        17/09/2024      9:41         286720 SearchFilterHost.exe
-a----        17/09/2024      9:41         966656 SearchIndexer.exe
-a----        17/09/2024      9:41         462848 SearchProtocolHost.exe
-a----        27/06/2023      6:43         394248 SECCNH64.exe
-a----        07/05/2022      7:19          61440 SecEdit.exe
-a----        27/06/2023      6:43        1445480 SECOCL64.exe
-a----        27/06/2023      6:43         997944 SECOMN64.exe
-a----        17/09/2024      9:41         118784 SecureBootEncodeUEFI.exe
-a----        17/09/2024      9:41        1131904 securekernel.exe
-a----        17/09/2024      9:42        1074696 securekernella57.exe
-a----        17/09/2024      9:41         116104 SecurityHealthHost.exe
-a----        17/09/2024      9:41         146168 SecurityHealthService.exe
-a----        17/09/2024      9:41         266240 SecurityHealthSystray.exe
-a----        17/09/2024      9:41        1191936 SensorDataService.exe
-a----        17/09/2024      9:41         102400 SensorRuntimeBroker.exe
-a----        17/09/2024      9:41         757720 services.exe
-a----        07/05/2022      7:20         104688 sessionmsg.exe
-a----        17/09/2024      9:41         147456 sethc.exe
-a----        07/05/2022      7:20          53248 setspn.exe
-a----        07/05/2022      7:19         155648 setupugc.exe
-a----        07/05/2022      7:20          81920 setx.exe
-a----        17/09/2024      9:41         106496 sfc.exe
-a----        17/09/2024      9:41        1493208 ShellAppRuntime.exe
-a----        07/05/2022      7:19          73728 shrpubw.exe
-a----        07/05/2022      7:19          53248 shutdown.exe
-a----        07/05/2022      7:19          98304 sigverif.exe
-a----        17/09/2024      9:42         430328 SIHClient.exe
-a----        17/09/2024      9:41         147456 sihost.exe
-a----        17/09/2024      9:41         675840 slui.exe
-a----        17/09/2024      9:41         630784 smartscreen.exe
-a----        07/05/2022      7:19         183232 smss.exe
-a----        17/09/2024      9:41         307296 SndVol.exe
-a----        17/09/2024      9:42         208896 SpaceAgent.exe
-a----        17/09/2024      9:41         108016 spaceman.exe
-a----        17/09/2024      9:41         229376 spaceutil.exe
-a----        17/09/2024      9:40         184320 SpatialAudioLicenseSrv.exe
-a----        17/09/2024      9:42         770048 Spectrum.exe
-a----        17/09/2024      9:41         925696 spoolsv.exe
-a----        17/09/2024      9:41         589824 SppExtComObj.Exe
-a----        17/09/2024      9:41        4769872 sppsvc.exe
-a----        07/05/2022      7:20          77824 SrTasks.exe
-a----        17/09/2024      9:41         180224 stordiag.exe
-a----        07/05/2022      7:19          79920 svchost.exe
-a----        22/12/2023     13:30          61440 sxstrace.exe
-a----        17/09/2024      9:42          67056 SyncAppvPublishingServer.exe
-a----        07/05/2022      7:20          69632 SyncHost.exe
-a----        17/04/2024     11:59          71024 SysResetErr.exe
-a----        07/05/2022      7:20         118784 systeminfo.exe
-a----        07/05/2022      7:19         102400 SystemPropertiesAdvanced.exe
-a----        07/05/2022      7:19         102400 SystemPropertiesComputerName.exe
-a----        07/05/2022      7:19         102400 SystemPropertiesDataExecutionPrevention.exe
-a----        07/05/2022      7:19         102400 SystemPropertiesHardware.exe
-a----        07/05/2022      7:19         102400 SystemPropertiesPerformance.exe
-a----        07/05/2022      7:19         102400 SystemPropertiesProtection.exe
-a----        07/05/2022      7:19         102400 SystemPropertiesRemote.exe
-a----        17/09/2024      9:42         542728 systemreset.exe
-a----        17/09/2024      9:41         728760 SystemSettingsAdminFlows.exe
-a----        17/09/2024      9:41         220536 SystemSettingsBroker.exe
-a----        17/09/2024      9:41          67544 SystemSettingsRemoveDevice.exe
-a----        17/09/2024      9:41         118784 SystemUWPLauncher.exe
-a----        07/05/2022      7:20         110592 tabcal.exe
-a----        07/05/2022      7:20          86016 takeown.exe
-a----        17/09/2024      9:41          77824 tar.exe
-a----        17/09/2024      9:41         113104 taskhostw.exe
-a----        07/05/2022      7:20         114688 taskkill.exe
-a----        07/05/2022      7:20         118784 tasklist.exe
-a----        17/09/2024      9:41        5513616 Taskmgr.exe
-a----        17/09/2024      9:41         878168 tcblaunch.exe
-a----        17/09/2024      9:41          86016 ThumbnailExtractionHost.exe
-a----        07/05/2022      7:20         344064 TieringEngineService.exe
-a----        07/05/2022      7:20          53248 timeout.exe
-a----        17/09/2024      9:41          73728 TokenBrokerCookies.exe
-a----        07/05/2022      7:19          90112 TpmInit.exe
-a----        17/09/2024      9:41         172032 TpmTool.exe
-a----        17/09/2024      9:41         122880 tpmvscmgr.exe
-a----        17/09/2024      9:41         143360 tpmvscmgrsvr.exe
-a----        07/05/2022      7:20         425984 tracerpt.exe
-a----        07/05/2022      7:20          94208 TSTheme.exe
-a----        17/09/2024      9:42         114688 TSWbPrxy.exe
-a----        07/05/2022      7:19         513368 ttdinject.exe
-a----        07/05/2022      7:19         230768 tttracer.exe
-a----        07/05/2022      7:20          73728 typeperf.exe
-a----        22/12/2023     13:30          71680 tzsync.exe
-a----        07/05/2022      7:19          61440 tzutil.exe
-a----        17/09/2024      9:40          66560 UCPDMgr.exe
-a----        07/05/2022      7:19          50520 ucsvc.exe
-a----        17/09/2024      9:42          55296 UevAppMonitor.exe
-a----        17/09/2024      9:41          69632 UIMgrBroker.exe
-a----        07/05/2022      7:19          65536 unlodctr.exe
-a----        06/05/2022     22:10         258048 unregmp2.exe
-a----        07/05/2022      7:19         150168 upfc.exe
-a----        17/09/2024      9:41          69632 UpgradeResultsUI.exe
-a----        22/12/2023     13:30          69632 upnpcont.exe
-a----        17/09/2024      9:42          81920 UPPrinterInstaller.exe
-a----        17/09/2024      9:41          71680 UserAccountBroker.exe
-a----        17/09/2024      9:41         151552 UserAccountControlSettings.exe
-a----        17/09/2024      9:41          69632 UserDataSource.exe
-a----        17/09/2024      9:41         131072 userinit.exe
-a----        17/09/2024      9:41          81920 UsoClient.exe
-a----        17/09/2024      9:41         172032 UtcDecoderHost.exe
-a----        17/09/2024      9:41         368640 Utilman.exe
-a----        22/12/2023     13:30         692224 vds.exe
-a----        07/05/2022      7:19          73728 vdsldr.exe
-a----        07/05/2022      7:19         189776 verifier.exe
-a----        17/09/2024      9:41         245760 verifiergui.exe
-a----        17/09/2024      9:41         315392 VoiceAccess.exe
-a----        07/05/2022      7:20         163840 vssadmin.exe
-a----        17/09/2024      9:41        1449984 VSSVC.exe
-a----        25/01/2024     22:52        2115216 vulkaninfo-1-999-0-0-0.exe
-a----        25/01/2024     22:52        2115216 vulkaninfo.exe
-a----        07/05/2022      7:19         221184 w32tm.exe
-a----        07/05/2022      7:20          61440 waitfor.exe
-a----        07/05/2022      7:20         344064 wbadmin.exe
-a----        17/09/2024      9:41        1572864 wbengine.exe
-a----        17/04/2024     11:59         126976 wecutil.exe
-a----        17/09/2024      9:41         628208 WerFault.exe
-a----        17/09/2024      9:41         216440 WerFaultSecure.exe
-a----        17/09/2024      9:41         275976 wermgr.exe
-a----        17/04/2024     11:59         282624 wevtutil.exe
-a----        07/05/2022      7:20         163840 wextract.exe
-a----        17/09/2024      9:42         987136 WFS.exe
-a----        07/05/2022      7:20          61440 where.exe
-a----        07/05/2022      7:20          94208 whoami.exe
-a----        07/05/2022      7:20         118784 wiaacmgr.exe
-a----        07/05/2022      7:20          57344 wiawow64.exe
-a----        22/12/2023     13:30         185840 wifitask.exe
-a----        22/12/2023     13:30         603520 wimserv.exe
-a----        17/09/2024      9:41         114688 WinBioDataModelOOBE.exe
-a----        17/09/2024      9:41          94208 Windows.WARP.JITService.exe
-a----        17/09/2024      9:42          77824 WindowsActionDialog.exe
-a----        17/09/2024      9:41          65536 WindowsUpdateElevatedInstaller.exe
-a----        17/09/2024      9:41         580048 wininit.exe
-a----        17/09/2024      9:41        1672648 winload.exe
-a----        17/09/2024      9:41         937984 winlogon.exe
-a----        17/09/2024      9:41        1290384 winresume.exe
-a----        07/05/2022      7:19          69632 winrs.exe
-a----        07/05/2022      7:19          53248 winrshost.exe
-a----        22/12/2023     13:31        2748416 WinSAT.exe
-a----        17/09/2024      9:42         327968 wkspbroker.exe
-a----        17/09/2024      9:41         425984 wksprt.exe
-a----        07/05/2022      7:19         118784 wlanext.exe
-a----        17/09/2024      9:41         158544 wlrmdr.exe
-a----        07/05/2022     12:28        1564672 WMPDMC.exe
-a----        22/12/2023     13:31         118784 WorkFolders.exe
-a----        17/09/2024      9:40        1212200 WpcMon.exe
-a----        17/09/2024      9:40         311296 WpcTok.exe
-a----        07/05/2022     12:28          53248 WPDShextAutoplay.exe
-a----        17/09/2024      9:41         385024 wpr.exe
-a----        07/05/2022      7:19          98304 WSCollect.exe
-a----        17/09/2024      9:41         204800 wscript.exe
-a----        17/09/2024      9:42         200704 wsl.exe
-a----        17/09/2024      9:42         135168 wslg.exe
-a----        22/12/2023     13:30          61440 WSManHTTPConfig.exe
-a----        22/12/2023     13:30          65536 wsmprovhost.exe
-a----        07/05/2022      7:19          81920 wsqmcons.exe
-a----        22/12/2023     13:30          98304 WSReset.exe
-a----        17/09/2024      9:41         147824 wuauclt.exe
-a----        22/12/2023     13:30         191520 WUDFCompanionHost.exe
-a----        22/12/2023     13:30         307200 WUDFHost.exe
-a----        07/05/2022      7:19         188416 wusa.exe
-a----        17/09/2024      9:41        1054176 WWAHost.exe
-a----        17/09/2024      9:40          57344 XblGameSaveTask.exe
-a----        07/05/2022      7:20          73728 xcopy.exe
-a----        07/05/2022      7:20          90112 xwizard.exe
```


 


