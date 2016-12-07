# roles/rrp/files/processing_ansible_recipe_draft.md

## Variables

ansible_hostname: <target_host_name>

## get size of /boot

sudo df -h /boot

## Get firewall state

sudo shorewall status

## Get manufacturer

cat ../ace_fetched_files/{{ ansible_hostname }}/command_output/dmidecode.txt | grep Manufacturer | head -n1 | grep -o '[^: ]*$'
cat ../ace_fetched_files/ace-ws-59/command_output/dmidecode.txt | grep Manufacturer | head -n1 | grep -o '[^: ]*$'

cat ../ace_fetched_files/ace-ws-59/command_output/dmidecode.txt | grep "	Manufacturer:" | head -n2 | grep -o '[^: ]*$'
cat ../ace_fetched_files/ace-ws-59/command_output/dmidecode.txt | grep "	Manufacturer:" | head -n2
	Manufacturer:

## Get serial number

cat ../ace_fetched_files/ace-ws-10/command_output/dmidecode.txt | grep "Serial Number"
cat ../ace_fetched_files/{{ ansible_hostname }}/command_output/dmidecode.txt | grep "Serial Number" | head -n1 | cut -d: -f2
cat ../ace_fetched_files/ace-ws-10/command_output/dmidecode.txt | grep "Serial Number" | head -n1 | cut -d: -f2


## Get port speed

cat ../ace_fetched_files/{{ ansible_hostname }}/command_output/ethtool.txt | grep Speed | cut -d: -f2 | rev | cut -c 5- | rev
cat ../ace_fetched_files/ace-ws-59/command_output/ethtool.txt | grep Speed | cut -d: -f2 | rev | cut -c 5- | rev


