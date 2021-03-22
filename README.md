## Make Virtual Box VM Autostart

Linux <br>
Ubuntu 20.04 <br>
What you need to know <br>

#### VMNAME : Virtual Manchine Name that is registered with VirtualBox

user : Account to run as <br>
Edit /etc/default/virtualbox <br>

```sudo nano /etc/default/virtualbox```

Add the following few lines into the file

```#AutoStarting VMs``` <br>
```VBOXAUTOSTART_DB=/etc/vbox``` <br>
```VBOXAUTOSTART_CONFIG=/etc/vbox/autostart.cfg``` <br>

#### Create /etc/systemd/system/VMNAME.service
sudo nano /etc/systemd/system/VMNAME.service

```[Unit]``` <br>
```Description=vm1``` <br>
```After=network.target virtualbox.service``` <br>
```Before=runlevel2.target shutdown.target``` <br>
```[Service]``` <br>
```User=user``` <br>
```Group=vboxusers``` <br>
```Type=forking``` <br>
```Restart=no``` <br>
```TimeoutSec=5min``` <br>
```IgnoreSIGPIPE=no``` <br>
```KillMode=process``` <br>
```GuessMainPID=no``` <br>
```RemainAfterExit=yes``` <br>
```ExecStart=/usr/bin/VBoxManage startvm VMNAME --type headless``` <br>
```ExecStop=/usr/bin/VBoxManage controlvm VMNAME acpipowerbutton``` <br>
```[Install]``` <br>
```WantedBy=multi-user.target``` <br>

#### Reload Daemon

```sudo systemctl daemon-reload``` <br>

#### Test
```systemctl status VMNAME``` <br>

#### Start
```sudo systemctl start VMNAME``` <br>

#### Stop
```sudo systemctl stop VMNAME``` <br>

#### Enable
```sudo systemctl enable VMNAME``` <br>

#### Disable

sudo systemctl disable VMNAME``` <br>


by paulligocki https://www.paulligocki.com/make-virtual-box-vm-autostart/
