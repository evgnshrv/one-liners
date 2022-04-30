## One-liners and Short Manuals

In this repository I have collected useful one-liners and short manuals.

***

## One-liners

### Linux

Show audit.log in readable form:  
```sudo cat /var/log/audit/audit.log | perl -ne 'chomp; if ( /(.*msg=audit\()(\d+)(\.\d+:\d+.*)/ ) { $td = scalar localtime $2; print "$1$td$3\n"; }'```

Count number of clients connected to Chrony NTP server:  
```chronyc -a -n -m clients |wc -l```

Running a command on a group of servers with ansible:  
```ansible -m shell -a '<command>' <group_hosts_name> --ask-pass```

Rescan all drives to mount a new drive:  
```for host in /sys/class/scsi_host/*; do echo "- - -" | sudo tee $host/scan; ls /dev/sd* ; done```

Disk Speed Test:  
```sync; date; dd if=/dev/zero of=/data/tempfile bs=10M count=5000; sync; date```

### VMware

Find all VM snapshots:  
```get-vm | get-snapshot | Select-Object -Property vm,created,sizeGB,name,description | Export-Csv -Path C:\Users\$env:username\Desktop\snapshots.csv```

Search for all VMs created in the last 30 days:  
```Get-VIEvent -maxsamples 1000000 -Start (Get-Date).AddDays(-30) | where {$_.Gettype().Name-eq "VmCreatedEvent" -or $_.Gettype().Name-eq "VmBeingClonedEvent" -or $_.Gettype().Name-eq "VmBeingDeployedEvent"} |Sort CreatedTime -Descending |Select CreatedTime, UserName,FullformattedMessage |export-Csv "C:\scripts\createvm.csv" -NoTypeInformation```

Find all VMs that have been restarted in the last 24 hours (there is the word "restarted" in the logs):  
```Get-VIEvent -MaxSamples 100000 -Start (Get-Date).AddDays(-1) -Type Warning | Where {$_.FullFormattedMessage -match "restarted"} |select CreatedTime,FullFormattedMessage | sort CreatedTime –Descending```

Find a VM with a specific IP address:  
```Get-VM | Where-Object -FilterScript { $_.Guest.Nics.IPAddress -contains "AB.CD.EF.GH" }```

Find a VM with a specific MAC address:  
```
$report =@() 
Get-VM | Get-View | %{ 
 $VMname = $_.Name 
 $_.guest.net | where {$_.MacAddress -eq "AB:CD:EF:GH:IJ:KL"} | %{
        $row = "" | Select VM, MAC
        $row.VM = $VMname 
        $row.MAC = $_.MacAddress 
        $report += $row 
  } 
  } 
$report
```

### Windows

***

## Short manuals


