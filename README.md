# containerd-issue
Issue on containerd 1.6.9-1 as of last test.


## Example Output:
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
