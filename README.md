# choco_chef

* Windows AMIs ready bootstrap to BJC for compliance demos
*   Create and bootstrap commands to run from within your BJC workstation  
...Make sure and configure the Security Group and Subnet to map to your BJC instance  
* Example role you can add to your BJC environment and use to bootstrap a node with a CIS profile

## Current AMIs:
In us-west-2

windows 2016:  ami-0dffeb18491b15a05

windows 2012:


## Steps prep a base Windows AMI for bootstrapping with BJC:

* turn off windows firewall
* setup an administrative user/password to reference in bootstrap
* Run in powershell:

  winrm quickconfig -q  
  winrm set winrm/config '@{MaxTimeoutms="1800000"}'  
  winrm set winrm/config/service '@{AllowUnencrypted="true"}'  
  winrm set winrm/config/service/auth '@{Basic="true"}'  
  
  Set-Item wsman:localhost\client\trustedhosts -value * -force  
  Get-NetFirewallProfile | Set-NetFirewallProfile -Enabled False  

  net stop winrm
  sc.exe config winrm start=auto
  net start winrm

* Configure a hosts file with:

  172.31.54.11    automate.automate-demo.com automate  
  172.31.54.10    chef.automate-demo.com chef
