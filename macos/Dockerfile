# Build container based on
# https://podman-desktop.io/docs/podman/gpu

FROM fedora:42 as builder

RUN dnf -y install \
        cmake \
        g++ \
        git \
        glslc \
        make \
        mesa-vulkan-drivers \
        vulkan-headers \
        vulkan-loader \
        vulkan-loader-devel \
        vulkan-tools

COPY ./vulkan_minimal_compute /vulkan-demo
WORKDIR /vulkan-demo
RUN cmake -DCMAKE_BUILD_TYPE=Release . \
    && make

# Runtime container based on
# https://sinrega.org/2024-03-06-enabling-containers-gpu-macos/

FROM quay.io/slopezpa/fedora-vgpu

COPY --from=builder /vulkan-demo/vulkan_minimal_compute /vulkan_minimal_compute

# Shaders are accesssed in runtime
COPY ./vulkan_minimal_compute/shaders /shaders

CMD ["/vulkan_minimal_compute"]
