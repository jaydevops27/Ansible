# HAProxy Checking and Stopping Script

This Ansible playbook is designed to check the status of HAProxy on a remote host and stop it if it's active. Additionally, it updates the kernel, reboots the EC2 instance, and starts HAProxy again after the reboot.

## Prerequisites
- Ansible installed on the control node.
- Access to the target host via SSH.
- `PEMKEY PATH` should be set as an environment variable or passed as a GitLab variable.
- The `PEMKEY PATH` should point to the private key file (.pem) for SSH authentication.

## Usage
1. Update the `hosts` field in the playbook to specify the target host where HAProxy is running (`haproxy-host` in this example).
2. Update the `PEMKEY PATH` variable with the path to your SSH private key file.
3. Modify the `ansible_user` variable to specify the remote user on the target host.
4. Run the playbook using the `ansible-playbook` command.

## Playbook Explanation
1. **Load PEM key from GitLab variable**: Loads the PEM key from the environment or GitLab variable.
2. **Exit if PEM key is not provided**: Fails the playbook if the PEM key is not provided.
3. **Check HAProxy Status**: Checks the status of HAProxy on the remote host.
4. **Display HAProxy Status**: Displays the status of HAProxy.
5. **Stop HAProxy if active**: Stops HAProxy if it's active.
6. **Verify HAProxy Status after stopping**: Verifies that HAProxy is inactive after stopping.
7. **Update Kernel**: Installs the `git` package to update the kernel.
8. **Reboot EC2 instance asynchronously**: Reboots the EC2 instance asynchronously.
9. **Wait for instance to become reachable**: Waits for the instance to become reachable after reboot.
10. **Retry connection after reboot**: Retries SSH connection after reboot.
11. **Display current kernel versions**: Displays the kernel version before and after the update.
12. **Start HAProxy after reboot**: Starts HAProxy after the reboot.
13. **Check HAProxy Status after starting**: Checks the status of HAProxy after starting.
