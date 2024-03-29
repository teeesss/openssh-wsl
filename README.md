## openssh-wsl
### Allow SSH into your WSL environment from the local LAN through Windows system

On WSL run the following: <br>

Add/Remove openssh-server <br>
`sudo apt remove openssh-server` <br>
`sudo apt install openssh-server` <br>

`sudo vi /etc/ssh/sshd_config` <br>
Uncomment Port 22 -> #Port 22 to Port 22 <br>
Uncomment #PasswordAuthentication yes to PasswordAuthentication yes <br>

From PowerShell run the following commands: <br>
`netsh interface portproxy add v4tov4 listenaddress=192.168.0.30 listenport=2022 connectaddress=192.168.0.30 connectport=22` <br>
Change the information above based on the examples below: <br>
listenaddress=<windows_host_ip> <br>
listenport=<your_windows_listen_port_number> <br>
connectaddress=<wsl_internal_ip> <br>
connectport=<ssh_service_port_number> <br>

`netsh advfirewall firewall add rule name="forward port 2022 to 22" dir=in action=allow protocol=TCP localport=2022` <br>
Change the information above based on the examples below: <br>
name="<any_name>" <br>
dir=in <br>
action=allow <br>
protocol=TCP <br>
localport=<your_windows_listen_port_number> <br>

Connect to WSL from a system inside your network: <br>
`ssh <wsl_username>@<windows_ip> -p <windows_protproxy_listenport>`
Ex: `ssh wsl_username@192.168.0.100 -p 2022`







