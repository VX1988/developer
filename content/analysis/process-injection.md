---
title: Process Injection Note Analysis
type: docs
---

# Process Injection Newly Create Process

- Script Tap inside windows telemetry.
- Required admin priviledge. 
- If you run the program, the program already running.

```powershell
Get-EventSubscriber -SourceIdentifier "ProcessStarted" | Unregister-Event
$action = {
  $name = $event.SourceEventArgs.NewEvent.ProcessName
  $id = $event.SourceEventArgs.NewEvent.ProcessId
  $parent = $event.SourceEventArgs.NewEvent.ParentProcessID
  $CMD=(Get-CimInstance -ClassName Win32_Process| ? {$_.ProcessId -eq $event.SourceEventArgs.newevent.processID} | Select -exp CommandLine)
  $Parentname=(Get-CimInstance -ClassName Win32_Process| ? {$_.ProcessId -eq $event.SourceEventArgs.newevent.ParentProcessID} | Select -exp CommandLine)
  Write-Host "New Process Started : $parentname | $parent | $name | $id | $CMD"
}
Register-CimIndicationEvent -ClassName 'Win32_ProcessStartTrace' -SourceIdentifier "ProcessStarted" -Action $action
```