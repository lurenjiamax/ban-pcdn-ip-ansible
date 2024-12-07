## Playbook for Blocking PDCN CIDRs

You can use the `main.yml` playbook to block PDCN CIDRs on a Linux server with iptables, UFW, or CSF firewall installed. This playbook will automate the process of adding the necessary rules to block the specified CIDRs.

This playbook can be used multiple times, as it will first remove the previous rules by `xx_unblock.sh` script before adding the new rules.

### Example Usage

To run the playbook, use the following command:
```bash
ansible-playbook -i inventory main.yml <-k>
```

Use the `-k` flag if you need to enter the password for the remote user.

Replace `inventory` with your inventory file.

### Example Inventory

```yaml
vps:
  hosts:
    host1:  // If your host1 is already in your ssh config file. 
    host2:  // Otherwise, you should define the host here.
        ansible_host: 123.123.123.123
        ansible_user: root
```

### Variables

Ensure you define the following variables in your inventory or playbook:
- `firewall`: The firewall to use (`iptables`, `ufw`, or `csf`), default to `auto` with priority of ufw > csf > iptables
- `cidr_file_url`: The URL to the file containing the CIDRs to block, default to github.com/unclemcz/ban-pcdn-ip
- `cidr_file`: Where the CIDR file will be downloaded to, default to `/tmp/cidr_list.txt`
- `output_folder`: The folder where the output files will be saved, including the block and unblock scripts, default to `~/ban_pdcn`

### Troubleshooting

If something goes wrong, use the unblock script to remove the rules. The unblock script will be saved in the output folder, the default is `~/ban_pdcn/xx_unblock.sh`.

