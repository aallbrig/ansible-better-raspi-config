### "better" raspi config ansible galaxy role

I noticed an opportunity to create an ansible galaxy role to create an ansible interface for using the `raspi-config` GUI tool that ships with Raspbian.

Current ansible galaxy roles that exist represent only a limited number of operations that the `raspi-config` tool can perform. See the [`raspi-config` documentation](https://www.raspberrypi.org/documentation/configuration/raspi-config.md) to see a list of possible operations. Check out the _Methodology_ section to see how I'll be creating an ansible role interface for `raspi-config`.

#### Methodology
I've `scp`ed the latest version of the `raspi-config.sh` script into this repo (`./reference`). The methodology is to find something that the `raspi-config` script can do (e.g. "set up hostname", "set up locale", "set up wifi") and then find out how the `raspi-config.sh` script does it. Once you have found the code block(s) relevant to an operation, turn those shell commands into idiomatic ansible. See these [examples](https://github.com/aallbrig/k8s-pi-cluster/blob/master/ansible/playbooks/init-setup.yml#L24) for the result of such operation.

Why not `man raspi-config` to check for a command line interface? `raspi-config` exposes few operations via the CLI. It appears the rool was built largely for a GUI audience. I wasn't able to find documentation on the tool, which is why I turned to `cat`ing the `raspi-config` shell script in the first place.

