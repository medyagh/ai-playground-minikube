# Instructions

Build the image:

```console
make
```

Push the image to the registry:

```console
make push
```

Start the cluster:

```console
minikube start -d krunkit
kubectl apply -f daemon.yaml
kubectl apply -f demo.yaml
```

Check that the GPU is detected in the demo container:

```console
% kubectl exec pod/vulkan-demo -it -- vulkaninfo --summary | grep GPU
GPU0:
    deviceType         = PHYSICAL_DEVICE_TYPE_INTEGRATED_GPU
    deviceName         = Virtio-GPU Venus (Apple M2 Max)
GPU1:
```

Run the demo program:

```console
% kubectl exec pod/vulkan-demo -- sh -c 'time /vulkan_minimal_compute'

real    0m0.355s
user    0m0.314s
sys     0m0.016s
```
