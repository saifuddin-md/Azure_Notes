# Create an Ubuntu Virtual Machine in Microsoft Azure

A beginner-friendly, step-by-step lab for deploying an Ubuntu Server VM
in the Azure Portal, connecting with SSH, installing NGINX, and cleaning
up resources.

> **Cost warning:** Azure resources may incur charges. Check the
> estimated cost before deployment. When finished, deallocate the VM and
> delete the lab resource group if you no longer need it. Deallocating a
> VM does not delete its disks or every associated resource.

## Lab overview

You will create:

| Setting | Example |
|---|---|
| Resource group | `RG-Ubuntu-Lab` |
| Virtual machine | `Ubuntu-VM` |
| Operating system | Ubuntu Server 24.04 LTS |
| Region | A region near you, such as Central India if available |
| Authentication | SSH public key |
| Network | New virtual network and subnet |
| SSH | TCP port 22, restricted to your public IP |
| Web server (optional) | NGINX on TCP port 80 |

Names and options may vary slightly in the Azure Portal. VM sizes, image
versions, availability, and pricing depend on your subscription and
region.

## Prerequisites

-   An Azure account with an active subscription and permission to
    create resources.
-   A computer with an SSH client:
    -   Windows 10/11: OpenSSH in PowerShell (usually available by
        default).
    -   macOS or Linux: Terminal with `ssh`.
-   A safe location to store your SSH private key.
-   Access to the Azure Portal: <https://portal.azure.com/>

## 1. Open the Azure Portal

1.  Go to <https://portal.azure.com/>.
2.  Sign in.
3.  In the search bar, enter **Virtual machines**.
4.  Open **Virtual machines**.
5.  Select **Create** → **Azure virtual machine**.

## 2. Configure the Basics tab

Use the following example values:

## Azure Ubuntu VM Configuration

| Field | Example value |
|---|---|
| Subscription | Select your subscription |
| Resource group | Select **Create new**, enter `RG-Ubuntu-Lab` |
| Virtual machine name | `Ubuntu-VM` |
| Region | Choose a region near you, e.g. Central India if available |
| Availability options | No infrastructure redundancy required for this practice lab |
| Security type | Keep a supported default, such as Trusted launch, if available |
| Image | Ubuntu Server 24.04 LTS |
| VM architecture | x64, if asked |
| Size | Choose a small, low-cost size available in your region |
| Authentication type | SSH public key |
| Username | `azureuser` |
| SSH public key source | Generate new key pair, if this is your first lab key |
  -----------------------------------------------------------------------

For the SSH key pair name, use something recognizable, such as
`ubuntu-lab-key`.

**Important:** When Azure offers to download the private key, download
it and save it somewhere safe. The private key is a secret. Do not
upload it to GitHub, email it, or share it. Azure does not keep a copy
of your private key that you can download later.

## 3. Configure Disks

1.  Open the **Disks** tab.
2.  For a basic practice VM, choose a Standard SSD if available and
    affordable.
3.  Keep other settings at their defaults unless your lab requires
    otherwise.
4.  Continue to **Networking**.

The OS disk stores Ubuntu. Additional data disks can be attached later
if required.

## 4. Configure Networking

1.  Create a new virtual network, for example `VNet-Ubuntu`.
2.  Keep or create a subnet, for example `default`.
3.  Create a public IP only if you need to connect directly over the
    internet.
4.  For the network security group, use the portal's basic configuration
    or an existing NSG.
5.  Under inbound ports, allow **SSH (22)** only from **My IP address**
    or another trusted, narrow source range if the option is available.
6.  Do not expose SSH to `Any` / `0.0.0.0/0` for routine access.

If you use a private VM with no public IP, connect through an approved
private network path such as Azure Bastion or a VPN instead.

## 5. Configure Management and Review

1.  Open the **Management** tab.
2.  Consider enabling boot diagnostics for troubleshooting.
3.  Configure auto-shutdown if you want the VM to shut down on a
    schedule. Check the time zone.
4.  Leave other optional settings at their defaults for this
    introductory lab.
5.  Select **Review + create**.
6.  Review the configuration and estimated cost.
7.  Select **Create**.
8.  If prompted, download the private key and create the resource.
9.  Wait for deployment to complete, then select **Go to resource**.

## 6. Find the VM's Public IP Address

1.  Open `Ubuntu-VM` in the Azure Portal.
2.  On the **Overview** page, find **Public IP address**.
3.  Copy the address.

Use the actual address shown in your portal. The examples below use
placeholders.

## 7. Connect to Ubuntu with SSH

### Windows PowerShell

Move to the folder where you saved the downloaded `.pem` private key.
For example:

``` powershell
cd $HOME\Downloads
ssh -i .\ubuntu-lab-key.pem azureuser@YOUR_PUBLIC_IP
```

### macOS or Linux Terminal

If the key is in your Downloads folder:

``` bash
chmod 400 ~/Downloads/ubuntu-lab-key.pem
ssh -i ~/Downloads/ubuntu-lab-key.pem azureuser@YOUR_PUBLIC_IP
```

Replace `YOUR_PUBLIC_IP` with the VM's actual public IP address. If you
chose a different username or key filename, use those values instead.

On the first connection, SSH may ask whether you trust the host
fingerprint. Verify it using your organization's process or Azure
guidance before accepting it.

### If SSH does not connect

Check the following:

-   The VM is running.
-   You copied the correct public IP address.
-   The username is correct.
-   You are using the matching private key.
-   The NSG allows TCP port 22 from your current public IP.
-   Your local network permits outbound SSH.
-   The VM has a working network interface and route.

If your public IP changes, update the NSG source rule to your new
trusted IP.

## 8. Run Basic Ubuntu Commands

After connecting, run these commands one at a time:

``` bash
# Show Ubuntu release information
cat /etc/os-release

# Show the hostname
hostname

# Show IP addresses
ip addr

# Show CPU information
lscpu

# Show memory usage
free -h

# Show disk usage
df -h

# Show system uptime
uptime
```

Update package information and install available updates:

``` bash
sudo apt update
sudo apt upgrade -y
```

## 9. Optional: Install and Test NGINX

Install the NGINX web server:

``` bash
sudo apt install nginx -y
```

Check its service status:

``` bash
sudo systemctl status nginx
```

Test it from inside the VM:

``` bash
curl http://localhost
```

If the command returns the NGINX welcome page HTML, the web server is
responding locally.

### Allow temporary HTTP access in Azure

To view the welcome page from your own browser:

1.  In the Azure Portal, open the VM.
2.  Open **Networking** (or the associated network security group).
3.  Add an inbound security rule:
    -   Source: preferably your IP address for this lab.
    -   Source port ranges: `*`
    -   Destination: Any
    -   Service: HTTP, or destination port `80`
    -   Protocol: TCP
    -   Action: Allow
    -   Priority: an unused priority, for example `300`
    -   Name: `Allow-HTTP-Lab`
4.  Save the rule.
5.  In your browser, open `http://YOUR_PUBLIC_IP`.

Port 80 is unencrypted HTTP. This is suitable only for a basic
demonstration, not for sensitive information. Remove the inbound rule
when you no longer need public web access.

## 10. Common VM Management Tasks

In the Azure Portal, open the VM's **Overview** page.

  ## Azure VM Management Actions

| Action | What it does |
|---|---|
| Start | Starts a stopped VM |
| Restart | Reboots the VM |
| Stop | Stops the VM; check whether it is deallocated |
| Stop (deallocate) | Releases compute allocation |
| Resize | Changes the VM's size, subject to availability |
| Delete | Deletes the VM resource |

**Billing note:** Shutting down Ubuntu from inside the operating system
is not necessarily the same as deallocating the VM in Azure. For a lab
you are not using, use the Azure Portal's **Stop** action and confirm
the status is **Stopped (deallocated)**. Managed disks and some other
resources can still incur charges.

## 11. Clean Up the Lab

When you have finished and no longer need the resources:

1.  In the Azure Portal, open **Resource groups**.
2.  Select `RG-Ubuntu-Lab`.
3.  Check that it contains only resources you intend to remove.
4.  Select **Delete resource group**.
5.  Enter the resource group name to confirm.
6.  Select **Delete**.

Deleting the resource group removes its contained resources, including
the VM, disks, network resources, and public IPs that belong to it. Make
sure you do not keep any data you need before deleting it.

## 12. Troubleshooting

### `Permission denied (publickey)`

-   Confirm the SSH username.
-   Confirm that you selected the matching private key.
-   On macOS/Linux, run `chmod 400` on the key.
-   Check that the VM was configured with the public key that matches
    your private key.

### Connection timed out

-   Confirm the VM is running.
-   Check the public IP.
-   Check the NSG inbound rule for TCP 22 and its source range.
-   Confirm that your current public IP matches the allowed source.

### NGINX page does not open

-   Run `sudo systemctl status nginx`.
-   Run `curl http://localhost` on the VM.
-   Confirm the NSG allows inbound TCP 80 from your IP.
-   Confirm you are browsing to `http://`, not `https://`, for this
    basic test.

## 13. Practical Lab Checklist

-   [ ] Sign in to the Azure Portal.
-   [ ] Create `RG-Ubuntu-Lab`.
-   [ ] Select Ubuntu Server 24.04 LTS.
-   [ ] Choose an affordable VM size.
-   [ ] Generate and safely save an SSH private key.
-   [ ] Configure a VNet and subnet.
-   [ ] Restrict SSH access to a trusted IP.
-   [ ] Deploy the VM.
-   [ ] Copy the public IP address.
-   [ ] Connect using SSH.
-   [ ] Run the Linux information commands.
-   [ ] Install and test NGINX (optional).
-   [ ] Add and later remove the temporary HTTP rule (optional).
-   [ ] Stop and deallocate the VM.
-   [ ] Delete the lab resource group when finished.

## Official Microsoft documentation

-   [Create a Linux virtual machine in the Azure
    Portal](https://learn.microsoft.com/azure/virtual-machines/linux/quick-create-portal)
-   [Connect to a Linux VM using
    SSH](https://learn.microsoft.com/azure/virtual-machines/linux-vm-connect)
-   [Azure Virtual Machines
    documentation](https://learn.microsoft.com/azure/virtual-machines/)
-   [Azure Network Security
    Groups](https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview)

------------------------------------------------------------------------

**Lab complete:** You have practiced deploying an Ubuntu VM, connecting
securely with SSH, running Linux commands, optionally hosting a simple
NGINX page, and cleaning up Azure resources.
