# MIG Support in OpenShift Container Platform

## Introduction

NVIDIA Multi-Instance GPU (MIG) is useful anytime you have an application that does not require the full power of an entire GPU. The NVIDIA Ampere architecture's MIG feature allows you to split your hardware resources into multiple GPU instances, each exposed to the operating system as an independent CUDA-enabled GPU. The NVIDIA GPU Operator MIG feature support for the A100 and A30 Ampere cards. These GPU instances are designed to support multiple independent CUDA applications (up to 7), so they operate completely isolated from each other using dedicated hardware resources.

The compute units of the GPU, in addition to its memory, can be partitioned into multiple MIG instances. Each of these instances presents as a stand-alone GPU device from the system perspective and can be bound to any application, container, or virtual machine running on the node.

From the perspective of the software consuming the GPU each of these MIG instances looks like its own individual GPU.

## MIG geometry

The NVIDIA GPU Operator enables OpenShift Container Platform administrators to dynamically reconfigure the geometry of the MIG partitioning. The geometry of the MIG partitioning is how hardware resources are bound to MIG instances, so it directly influences their performance and the number of instances that can be allocated. The A100-40GB, for example, has eight compute units and 40 GB of RAM. When the MIG mode is enabled, the eighth instance is reserved for resource management.

The table below provides a summary of the MIG instance properties of the NVIDIA A100-40GB product:

| Profile | Memory | Compute Units | Maximum number of homogeneous instances |
|---------|--------|---------------|----------------------------------------|
| 1g.5gb  | 5 GB   | 1             | 7                                      |
| 2g.10gb | 10 GB  | 2             | 3                                      |
| 3g.20gb | 20 GB  | 3             | 2                                      |
| 4g.20gb | 20 GB  | 4             | 1                                      |
| 7g.40gb | 40 GB  | 7             | 1                                      |

In addition to homogeneous instances, some heterogeneous combinations can be chosen. See the [Multi-Instance GPU User Guide documentation](https://docs.nvidia.com/datacenter/tesla/mig-user-guide/) for an exhaustive listing.

Here is an example, again for the A100-40GB, with heterogeneous (or "mixed") geometries:

- 2x 1g.5gb
- 1x 2g.10gb
- 1x 3g.20gb

## Prerequisites

The deployment workflow requires these prerequisites.

1. You already have a OpenShift Container Platform cluster up and running with access to at least one MIG-capable GPU.

2. You have followed the guidance in Installation and Upgrade Overview on OpenShift proceeding as far as creating the cluster policy `<create-cluster-policy>`.

> **Note**
>
> The node must be free (drained) of GPU workloads before any reconfiguration is triggered. For guidance on draining a node see, the OpenShift Container Platform documentation [Understanding how to evacuate pods on nodes](https://docs.openshift.com/container-platform/latest/nodes/nodes/nodes-nodes-working.html#nodes-nodes-working-evacuating_nodes-nodes-working).

## Configuring MIG Devices in OpenShift

### MIG advertisement strategies

The NVIDIA GPU Operator exposes GPUs to Kubernetes as extended resources that can be requested and exposed into Pods and containers. The first step of the MIG configuration is to decide what **Strategy** you want. The advertisement strategies are described here:

**Single** defines a homogeneous advertisement strategy, with MIG instances exposed as usual GPUs. This strategy exposes the MIG instances as `nvidia.com/gpu` resources, identically, as usual non-MIG capable (or with MIG disabled) devices. In this strategy, all the GPUs in a single node must be configured in a homogeneous manner (same number of compute units, same memory size). This strategy is best for a large cluster where the infrastructure teams can configure "node pools" of different MIG geometries and make them available to users. Another advantage of this strategy is backward compatibility where the existing application does not have to be modified to be scheduled this way.

Examples for the A100-40GB:
- 1g.5gb: 7 nvidia.com/gpu instances, or
- 2g.10gb: 3 nvidia.com/gpu instances, or
- 3g.20gb: 2 nvidia.com/gpuinstances, or
- 7g.40gb: 1 nvidia.com/gpu instances

**Mixed** defines a heterogeneous advertisement strategy. There is no constraint on the geometry; all the combinations allowed by the GPU are permitted. This strategy is appropriate for a smaller cluster, where on a single node with multiple GPUs, each GPU can be configured in a different MIG geometry.

Examples for the A100-40GB:
- All the single configurations are possible
- A "balanced" configuration:
  - 1g.5gb: 2 nvidia.com/mig-1g.5gb instances, and
  - 2g.10gb: 1 nvidia.com/mig-2g.10gb instance, and
  - 3g.20gb: 1 nvidia.com/mig-3g.20gb instance

### Configuring MIG Profiles

When MIG is enabled, nodes are labeled with `nvidia.com/mig.config: all-disabled` by default. To use a profile on a node, update the label value with the desired profile, for example, `nvidia.com/mig.config=all-1g.10gb`.

Introduced in GPU Operator v26.3.0, MIG Manager generates the MIG configuration for a node at runtime from the available hardware. The configuration is generated on startup, discovering MIG profiles for each MIG-capable GPU on a node using NVIDIA Management Library (NVML), then writing it to a ConfigMap for each MIG-capable node in your cluster. The ConfigMap is named `<node-name>-mig-config`, where `<node-name>` is the name of each MIG-capable node. Each ConfigMap contains a complete mig-parted config, including `all-disabled`, `all-enabled`, per-profile configs such as `all-1g.10gb`, and `all-balanced` with device-filter support for mixed GPU types. When a new MIG-capable GPU is added to a node, the new GPU is automatically added to the ConfigMap.

If you need custom profiles, you can use a custom MIG configuration instead of the generated one. You can use the Helm chart to create a ConfigMap from values at install time, or create and reference your own ConfigMap. For an example, refer to [Creating and applying a custom MIG configuration](#creating-and-applying-a-custom-mig-configuration).

> **Note**
>
> Generated MIG configuration might not be available on older drivers, such as 535 branch GPU drivers, as they do not support querying MIG profiles when MIG mode is disabled. In those cases, the GPU Operator will use a static Configmap, `default-mig-parted-config`, for MIG profiles.

The following tables describe some supported configurations:

#### Single configuration

| GPU Type   | Custom label  | Profile  | MIG instances |
|------------|---------------|----------|---------------|
| A100-40GB  | all-1g.5gb    | 1g.5gb   | 7             |
|            | all-2g.10gb   | 2g.10gb  | 3             |
|            | all-3g.20gb   | 3g.20gb  | 2             |
|            | all-7g.40gb   | 7g.40gb  | 1             |
| A100-80GB  | all-1g.10gb   | 1g.10gb  | 7             |
|            | all-2g.20gb   | 2g.20gb  | 3             |
|            | all-3g.40gb   | 3g.40gb  | 2             |
|            | all-7g.80gb   | 7g.80gb  | 1             |
| A30-24GB   | all-1g.6gb    | 1g.6gb   | 4             |
|            | all-2g.12gb   | 2g.12gb  | 2             |
|            | all-4g.24gb   | 4g.24gb  | 1             |

#### Balanced configuration

| GPU Type  | Custom label  | Profile and MIG instances                    |
|-----------|---------------|----------------------------------------------|
| A100-40GB | all-balanced  | 1g.5gb: 2<br>2g.10gb:1<br>3g.20gb:1         |
| A100-80GB | all-balanced  | 1g.10gb:2<br>2g.20gb:1<br>3g.40gb:1         |
| A30-24GB  | all-balanced  | 1g.6gb: 2<br>2g.12gb:1                      |

### Set the MIG advertisement strategy and apply the MIG partitioning

Having decided on your advertisement strategy you need to set this by editing the default cluster policy and then apply the MIG partitioning profile.

For example to set the advertisement strategy to mixed and the MIG partitioning profile to 3x 2g.10gb MIG devices follow the step below:

1. In the OpenShift Container Platform CLI run the following:

```bash
$ STRATEGY=mixed && \
oc patch clusterpolicy/gpu-cluster-policy --type='json' -p='[{"op": "replace", "path": "/spec/mig/strategy", "value": '$STRATEGY'}]'
```

> **Note**
>
> This may take a while so be patient and wait at least 10-20 minutes before digging deeper into any form of troubleshooting.

2. In the OpenShift Container Platform web console, from the side menu, select **Ecosystem > Installed Operators** (for versions before 4.20, look for **Operators > Installed Operators**), then click the **NVIDIA GPU Operator**.

3. Select the **ClusterPolicy** tab. The status of the newly deployed ClusterPolicy **gpu-cluster-policy** for the **NVIDIA GPU Operator** displays `State:ready` once the installation succeeded.

4. Apply the desired MIG partitioning profile. To configure 3x 2g.10gb MIG devices run the following:

```bash
$ MIG_CONFIGURATION=all-2g.10gb && \
oc label node/$NODE_NAME nvidia.com/mig.config=$MIG_CONFIGURATION --overwrite
```

5. Wait for the `mig-manager` to perform the reconfiguration:

```bash
$ oc -n nvidia-gpu-operator logs ds/nvidia-mig-manager --all-containers -f --prefix=true
```

The status of the reconfiguration should change from success → pending → success.

6. Verify the new configuration is applied:

```bash
$ oc get pods -n nvidia-gpu-operator -lapp=nvidia-driver-daemonset -owide
```

Select the name of the Pod on the MIG GPU enabled node and run the following:

```bash
$ oc rsh -n nvidia-gpu-operator $POD_NAME nvidia-smi mig -lgi
```

```
+----------------------------------------------------+
| GPU instances:                                      |
| GPU  Name             Profile  Instance  Placement |
|                       ID       ID        Start:Size|
|====================================================|
|   0  MIG 2g.10gb        19       3         4:2     |
+----------------------------------------------------+
|   0  MIG 2g.10gb        19       5         0:2     |
+----------------------------------------------------+
|   0  MIG 2g.10gb        19       6         2:2     |
+----------------------------------------------------+
```

With the profile in step 4 applied the A100 is configured into 3 MIG devices.

7. Check the node has been labeled:

```bash
$ oc get nodes/$NODE_NAME --show-labels | tr ',' '\n' | grep nvidia.com
```

with labels:

```
nvidia.com/gpu.present=true
nvidia.com/cuda.driver.major=470
nvidia.com/cuda.driver.minor=57
nvidia.com/cuda.driver.rev=02
nvidia.com/cuda.runtime.major=11
nvidia.com/cuda.runtime.minor=4
nvidia.com/gpu.compute.major=8
nvidia.com/gpu.compute.minor=0
nvidia.com/gpu.count=1
nvidia.com/gpu.family=ampere
nvidia.com/gpu.machine=...
nvidia.com/gpu.memory=40536
nvidia.com/gpu.product=NVIDIA-A100-SXM4-40GB
nvidia.com/mig-2g.10gb.count=3
nvidia.com/mig-2g.10gb.engines.copy=2
nvidia.com/mig-2g.10gb.engines.decoder=1
nvidia.com/mig-2g.10gb.engines.encoder=0
nvidia.com/mig-2g.10gb.engines.jpeg=0
nvidia.com/mig-2g.10gb.engines.ofa=0
nvidia.com/mig-2g.10gb.memory=9984
nvidia.com/mig-2g.10gb.multiprocessors=28
nvidia.com/mig-2g.10gb.slices.ci=2
nvidia.com/mig-2g.10gb.slices.gi=2
nvidia.com/mig.config.state=success
nvidia.com/mig.config=all-2g.10gb
nvidia.com/mig.strategy=mixed
[...]
```

> **Note**
>
> The extract above shows the strategy is set to mixed with the MIG configuration set to `all-2g.10gb`.

8. Verify that the MIG instances are exposed:

```bash
$ oc get node/$NODE_NAME -ojsonpath={.status.allocatable} | jq . | grep nvidia
```

```
"nvidia.com/mig-2g.10gb": "3",
```

> **Note**
>
> You can ignore values set to 0.

### Creating and applying a custom MIG configuration

Follow the guidance below to create a new slicing profile.

1. Prepare a custom `configmap` resource file for example `custom_configmap.yaml`. Use the configmap as guidance to help you build that custom configuration. For more documentation about the file format see [mig-parted](https://github.com/NVIDIA/mig-parted).

> **Note**
>
> For a list of all supported combinations and placements of profiles on A100 and A30, refer to the section on [supported profiles](https://docs.nvidia.com/datacenter/tesla/mig-user-guide/index.html#supported-profiles).

2. Create the custom configuration within the `nvidia-gpu-operator` namespace:

```bash
$ CONFIG_FILE=/path/to/custom_configmap.yaml && \
oc create configmap custom-mig-parted-config \
  --from-file=config.yaml=$CONFIG_FILE \
  -n nvidia-gpu-operator
```

3. Edit the cluster policy and enter the name of the config map in the field `spec.migManager.config.name`:

```bash
$ oc edit clusterpolicy
spec:
  migManager:
    config:
      name: custom-mig-parted-config
```

4. Label the node with this newly created profile following the guidance in [Set the MIG advertisement strategy and apply the MIG partitioning](#set-the-mig-advertisement-strategy-and-apply-the-mig-partitioning).

## Example: Mixed MIG strategy

### Introduction and default MIG configuration

For each MIG configuration, you specify a strategy and a MIG configuration label.

This example shows how to configure a `mixed` strategy with the `all-balanced` configuration on one NVIDIA DGX H100 host with 8 x H100 80GB GPUs. The DGX H100 host runs a single node installation of OpenShift.

By default, MIG is disabled and is configured with the `single` strategy:

```bash
$ oc describe node | grep nvidia.com/mig
```

Example Output:

```
nvidia.com/mig.capable=true
nvidia.com/mig.config=all-disabled
nvidia.com/mig.config.state=success
nvidia.com/mig.strategy=single
```

With the default configuration, the host supports up to 8 pods with GPUs:

```bash
$ oc describe node | egrep "Name:|Roles:|Capacity|nvidia.com/gpu|Allocatable:|Requests"
```

Example Output:

```
Name:               myworker.redhat.com
Roles:              control-plane,master,worker
Capacity:
  nvidia.com/gpu:     8
Allocatable:
  nvidia.com/gpu:     8
Resource            Requests    Limits
  nvidia.com/gpu      0           0
```

### Procedure

The following steps show how to apply the `mixed` strategy with the MIG configuration label `all-balanced`.

With this strategy and label, each H100 GPU enables these MIG profiles:

- 2 x 1g.10gb
- 1 x 2g.20gb
- 1 x 3g.40gb

For the NVIDIA DGX H100 that has 8 H100 GPUs, performing the steps results in the following GPU capacity on the cluster:

- 16 x 1g.10gb (8 x 2)
- 8 x 2g.20gb (8 x 1)
- 8 x 3g.40gb (8 x 1)

1. Specify the host name, strategy, and configuration label in environment variables:

```bash
$ NODE_NAME=myworker.redhat.com
$ STRATEGY=mixed
$ MIG_CONFIGURATION=all-balanced
```

2. Apply the strategy:

```bash
$ oc patch clusterpolicy/gpu-cluster-policy --type='json' \
  -p='[{"op": "replace", "path": "/spec/mig/strategy", "value": '$STRATEGY'}]'
```

3. Label the node with the configuration label:

```bash
$ oc label node $NODE_NAME nvidia.com/mig.config=$MIG_CONFIGURATION --overwrite
```

MIG manager applies a `mig.config.state` label to the GPU and then terminates all the GPU pods in preparation to enable MIG mode and configure the GPU into the specified configuration.

4. Optional: Verify that MIG manager configured the GPUs:

```bash
$ oc describe node | grep nvidia.com/mig.config
```

Example Output:

```
nvidia.com/mig.config=all-balanced
nvidia.com/mig.config.state=success
```

5. Confirm that the GPU resources are available:

```bash
$ oc describe node | egrep "Name:|Roles:|Capacity|nvidia.com/gpu:|nvidia.com/mig|Allocatable:|Requests"
```

The following sample output shows the expected 32 GPU resources:

- 16 x 1g.10gb
- 8 x 1g.10gb
- 8 x 3g.40gb

```
Name:               myworker.redhat.com
Roles:              control-plane,master,worker
Capacity:
  nvidia.com/gpu:            0
  nvidia.com/mig-1g.10gb:   16
  nvidia.com/mig-2g.20gb:    8
  nvidia.com/mig-3g.40gb:    8
Allocatable:
  nvidia.com/gpu:            0
  nvidia.com/mig-1g.10gb:   16
  nvidia.com/mig-2g.20gb:    8
  nvidia.com/mig-3g.40gb:    8
Resource                   Requests    Limits
  nvidia.com/mig-1g.10gb     0           0
  nvidia.com/mig-2g.20gb     0           0
  nvidia.com/mig-3g.40gb     0           0
```

6. Optional: Start a pod to run the `nvidia-smi` command and display the GPU resources.

   a. Start the pod:

   ```bash
   $ cat <<EOF | oc apply -f -
   apiVersion: v1
   kind: Pod
   metadata:
     name: command-nvidia-smi
   spec:
     restartPolicy: Never
     containers:
     - name: cuda-container
       image: nvcr.io/nvidia/cuda:12.1.0-base-ubi8
       command: ["/bin/sh","-c"]
       args: ["nvidia-smi"]
   EOF
   ```

   b. Confirm the pod ran successfully:

   ```bash
   $ oc get pods
   ```

   Example Output:

   ```
   NAME                  READY   STATUS      RESTARTS   AGE
   command-nvidia-smi    0/1     Completed   0          3m34s
   ```

   c. Confirm that the `nvidia-smi` output includes 32 MIG devices:

   ```bash
   $ oc logs command-nvidia-smi
   ```

   d. Delete the sample pod:

   ```bash
   $ oc delete pod command-nvidia-smi
   ```

   Example Output:

   ```
   pod "command-nvidia-smi" deleted
   ```

## Example: Single MIG strategy

This example shows how to configure a `single` strategy with the `all-3g.40gb` configuration on one NVIDIA DGX H100 host with 8 x H100 80GB GPUs. The DGX H100 host runs a single node installation of OpenShift.

For information about the initial default MIG configuration and viewing it, refer to the beginning of [Example: Mixed MIG strategy](#example-mixed-mig-strategy).

1. Specify the host name, strategy, and configuration label in environment variables:

```bash
$ NODE_NAME=myworker.redhat.com
$ STRATEGY=single
$ MIG_CONFIGURATION=all-3g.40gb
```

2. Apply the strategy:

```bash
$ oc patch clusterpolicy/gpu-cluster-policy --type='json' \
  -p='[{"op": "replace", "path": "/spec/mig/strategy", "value": '$STRATEGY'}]'
```

3. Label the node with the configuration label:

```bash
$ oc label node $NODE_NAME nvidia.com/mig.config=$MIG_CONFIGURATION --overwrite
```

MIG manager applies a `mig.config.state` label to the GPU and then terminates all the GPU pods in preparation to enable MIG mode and configure the GPU into the specified configuration.

4. Confirm that the GPU resources are available:

```bash
$ oc describe node | egrep "Name:|Roles:|Capacity|nvidia.com/gpu:|nvidia.com/mig|Allocatable:|Requests"
```

The following sample output shows the expected 16 GPUs:

```
Name:               myworker.redhat.com
Roles:              control-plane,master,worker
Capacity:
  nvidia.com/gpu:            16
  nvidia.com/mig-1g.10gb:     0
  nvidia.com/mig-2g.20gb:     0
  nvidia.com/mig-3g.40gb:     0
Allocatable:
  nvidia.com/gpu:            16
  nvidia.com/mig-1g.10gb:     0
  nvidia.com/mig-2g.20gb:     0
  nvidia.com/mig-3g.40gb:     0
Resource                   Requests    Limits
  nvidia.com/mig-1g.10gb     0           0
  nvidia.com/mig-2g.20gb     0           0
  nvidia.com/mig-3g.40gb     0           0
```

5. Optional: Start a pod to run the `nvidia-smi` command and display the GPU resources (follow steps from previous example).

## Running a sample GPU application

Let's run a simple CUDA sample, in this case `vectorAdd` by requesting a GPU resource as you would normally do in Kubernetes.

If the cluster is configured with the `mixed` advertisement strategy.

1. Request the MIG instance with `nvidia.com/mig-2g.10gb: 1` as follows:

---

**Privacy Policy** | **Your Privacy Choices** | **Terms of Service** | **Accessibility** | **Corporate Policies** | **Product Security** | **Contact**

Copyright © 2020-2026, NVIDIA Corporation.
