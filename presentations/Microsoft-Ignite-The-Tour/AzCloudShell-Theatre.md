# Master the Cloud with Azure Cloud Shell

You already know PowerShell is the key to on-premises workloads. Now take the power of the shell into the Cloud with Azure Cloud Shell. This demo-packed session will introduce you to Azure Cloud Shell, and provide plenty of tips to be immediately effective in using the command line to manage your Azure resources from anywhere.

## Pre-Reqs

Deploy Windows VM
Deploy Linux VM
Azure Account Extension -VS Code

Shell with GIT already authenticated
## Demos

1. Intro to cloud shell (2)
   1. Marketing Slides
2. Where is Cloud Shell Available?
   1. Azure Portal
   2. Visual Studio Code
   3. shell.azure.com
3. Walk through initial setup (2)
   1. Add drive through advanced settings
   2. Run through taskbar options
   3. View Storage
   4. Upload Script
   5. Open code with {}
4. Exploring the Shell
   1. Dir to view subs
   2. Discuss Azure Drive
   3. Explore down to VMs
5. find Az commands (2)
   1. Find AZ* and AzureAD*
6. Explore to $Home
   1. create directory
   2. Create script in code and save here
   3. Open script
7. Edit Script in VS Code Editor (2)
8. Remote into VMs

```PowerShell
# Enable VMs
$win = 'vm-windows-01'
$lnx = 'vm-linux-01'
$rsg = 'mitt-cloudshell-demo'
$cred = Get-credential

# Windows VM
Enable-AzVMPSRemoting -Name $win -ResourceGroupName $rsg -Protocol https -OsType Windows

# Linux VM
Enable-AzVMPSRemoting -Name $lnx -ResourceGroupName $rsg -Protocol ssh -OsType Linux

# Fan Out to VMs
# Windows VM
Invoke-AzVMCommand -Name $win -ResourceGroupName $rsg -ScriptBlock {get-service win*} -Credential $cred

# Linux VM
Invoke-AzVMCommand -Name $lnx -ResourceGroupName $rsg -ScriptBlock {uname -a} -UserName michael -KeyFilePath /home/michael/.ssh/id_rsa

# Connect to VM with Remoting
Enter-AzVM -name $win -ResourceGroupName $rsg -Credential $cred
whoami
get-service | where status -eq stopped
```

1. Deploy resources from Azure-Samples (2)
   ```PowerShell

   New-AzResourceGroup -Name 'cloudshell-demo-02' -location 'westeurope'

get-azResource -ResourceGroupName 'cloudshell-demo-02'

New-AzureRmResourceGroupDeployment -Name 'cloudshell-demo' -ResourceGroupName 'cloudshell-demo-02' -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-automatic-static-ip/azuredeploy.json   -AsJob

get-job | format-list

get-azResource -ResourceGroupName 'cloudshell-demo-02'

get-azResource -ResourceGroupName 'cloudshell-demo-02' | Format-Table
```
2. Use GIT to clone demo folder w/ Scripts (2)
   1. 42 cd $Home
  43 dir
  44 cd ./clouddrive/
  45 dir
  46 mkdir github
  47 cd ./github/
  48 git clone https://github.com/themichaelbender-ms/demos.git
  49 git status
  50 dir
  51 cd demos
  52 git status
  53 git branch
  54 git checkout -b demobranch-cs
  55 code
  56 dir
  57 git status
  58 git pull
  59 git checkout master
  60 git pull
  61 git status
  62 git checkout demobranch-cs
  63 git status
  64 dir
  65 git checkout master
  66 dir
  67 git branch -d demobranch-cs
  68 git branch -b demo-cs
  69 git checkout -b demo-cs
  70 git status
  71 dir
  72 cd ./demoscripts
  73 dir
  74 code ./get-stoppedServices.ps1
  75 git status
  76 git add .
  77 git commit -m 'Script Update'
  78 git commit -m 'Script Update' -a
  79 git push
  80 git push --set-upstream origin demo-cs
3.  Show Microsoft Learn module on X and show Azure Cloud Shell (2)
4.  Close with Slide of iphone screen accessing cloud shell (1)