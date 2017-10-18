#!/bin/bash
for ip in 192.168.56.{195..197}; do
    sshpass -p 'vagrant' ssh-copy-id -f -i ~/.ssh/id_rsa.pub vagrant@$ip
done