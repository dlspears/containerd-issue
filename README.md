# containerd-issue
Issue on containerd 1.6.9-1 as of last test.


### Example Output:
```
    default: Events:
    default:   Type     Reason       Age               From               Message
    default:   ----     ------       ----              ----               -------
    default:   Normal   Scheduled    2m                default-scheduler  Successfully assigned default/containerd-test to kind-control-plane
    default:   Warning  FailedMount  119s              kubelet            MountVolume.SetUp failed for volume "kube-api-access-8nchj" : failed to sync configmap cache: timed out waiting for the condition
    default:   Normal   Pulling      118s              kubelet            Pulling image "docker.io/openstackhelm/libvirt:latest-ubuntu_focal"
    default:   Normal   Pulled       90s               kubelet            Successfully pulled image "docker.io/openstackhelm/libvirt:latest-ubuntu_focal" in 27.719491688s
    default:   Normal   Created      90s               kubelet            Created container containerd-test
    default:   Normal   Started      89s               kubelet            Started container containerd-test
b": OCI runtime exec failed: exec failed: unable to start container process: error adding pid 1710 to cgroups: failed to write 1710: open /sys/fs/cgroup/cpu,cpuacct/docker/ebc274bdf234ef20828c49560c12c912c47ba8e73cd1ec30ccac42efd8c65716/kubelet.slice/kubelet-kubepods.slice/kubelet-kubepods-pod82a2a707_2fe8_4feb_9fea_43ad1530dbf2.slice/cri-containerd-d0f9fb9650e5b1697b619fa690e51fe4289292b06deb0d5487eafd782c2e8c1e.scope/cgroup.procs: no such file or directory: unknown
```

## Workaround/fix is use cgroups v2
Changing system to use cgroups v2 resolves the issue. Adding `systemd.unified_cgroup_hierarchy=1 cgroup_no_v1=all` to `/etc/default/grub` to the arguments for variable `GRUB_CMDLINE_LINUX` then run `update-grub` followed by a reboot resolves the issue.

## System Information

**OS**: 
```
Ubuntu 18.04
```
**Kernel**: 
```
4.15.0-167-generic
```
**Systemd**: 
```
systemd 237
+PAM +AUDIT +SELINUX +IMA +APPARMOR +SMACK +SYSVINIT +UTMP +LIBCRYPTSETUP +GCRYPT +GNUTLS +ACL +XZ +LZ4 +SECCOMP +BLKID +ELFUTILS +KMOD -IDN2 +IDN -PCRE2 default-hierarchy=hybrid
```
**Runc**:
```
runc version 1.1.4
commit: v1.1.4-0-g5fd4c4d
spec: 1.0.2-dev
go: go1.18.7
libseccomp: 2.5.1
```
**Containerd**:
```
containerd containerd.io 1.6.9 1c90a442489720eec95342e1789ee8a5e1b9536f
```
**Containerd config**:
```
#   Copyright 2018-2022 Docker Inc.

#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at

#       http://www.apache.org/licenses/LICENSE-2.0

#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.

disabled_plugins = ["cri"]

#root = "/var/lib/containerd"
#state = "/run/containerd"
#subreaper = true
#oom_score = 0

#[grpc]
#  address = "/run/containerd/containerd.sock"
#  uid = 0
#  gid = 0

#[debug]
#  address = "/run/containerd/debug.sock"
#  uid = 0
#  gid = 0
#  level = "info"
```

**Kind**:
```
kind version 0.17.0
```
### Installed packages
[distro-packages.txt](distro-packages.txt)
