2026/06/11
* **I removed the ISO from the disk drive to prevent it from installing all over again but I ran into a problem a few days later when trying to boot the pfsense vm up. 
The vm would freeze on 'cd0: Attempt to query device size failed:NOT READY, Medium not present.
I tried removing the drive from the boot options and rebooted the vm a couple of times and it went through. I  read that inserting a disk in the drive would fix this issue.**

I installed lubuntu to manage pfsense, but when i tried to ping the pfsense vm. I got nothing. I ran "ip addr" in the
terminal and found that i didn't have an ip address. I then manually assigned the vm an address of "10.0.0.3" as a test and
sure enough, when I ping "10.0.0.1" there's a connection. But I still cannot access the web interface.
Edit: While setting up the interface IP address for LAN again I think i messed something up with DHCP so i reconfigured it with the same information while double checking.
Edit: I realised while manually assigning an IP address to management vm, I gave it an ip address that was outside the scope I had set for dhcp on pfsense.
I then set the network  back to  automatic and ran "ip dhclient -v -r" to release the old IP address and then ran "ip dhclient -v" to request a new IP, which came back as "10.0.0.10"
Edit: That fixed my problem, I am able to log in now.

# host machine network bridge issues: SOLVED! 
2026/07/01 - After some time away from this lab, when coming back and trying to run my pfsense VM, I ran into an error "Error starting domain: Cannot get interface MTU on 'br-lan': No such device.
    - Attempted restarting host machine, problem remained.
    - Attempted running "systemctl restart libvirtd", error still present
    - Attempted running the command "sudo systemctl restart systemd-networkd" but the problem
      persisted.
    - Ran the command "nmtui" and edited the bridge connection from brLAN to br-lan, problem persists.
    - Suspecting ethernet cable not being plugged in is the root of this problem.
        - Plugging in cable did not fix the issue.
2026/07/02 
    - running ip link, br-lan did not show up anymore so I created it from scratch again. I identified my laptops ethernet port using ip link,
      "eno1" and then I created the bridge using "ip link name br-lan type bridge; ip link set dev br-lan up.
    - added the the physical port to the bridge, "sudo ip link set dev eno1 master br-lan"
    - Then brought both interfaces up,'ip link set dev br-lan up; sudo ip link dev eno1 up'.
    - since the bridge was already assigned on both the virtual hardware details for the pfsense VM and the manangement VM, I ran them both again and they started right up.
    
2026/07/03
    - Turned on the host machine today and the bridge is gone again, looked up online and found that ip link command does not create a persistent bridge,
    - ran these commands:
        - creating the persistent bridge: sudo nmcli conn add type bridge con-name br-lan ifname br-lan
        - binding the physical ethernet interface to the bridge as a slave: sudo nmcli conn add type ethernet con-name br-lan-slave ifname eno1 master br-lan
        - enabling the bridge connection: sudo nmcli conn up br-lan
