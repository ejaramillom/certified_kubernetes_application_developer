# Containers

- provide a method to run applications in full isolation
- to provide the isolation, linux kernel namespaces are used
- to provide all dependencies for running the application, a container is started from an image
- container images typically are obtained from a registry
- container images are highly standardized and can be used on stand-alone computers as well as in cloud

## Containers runtime 

- a container runtime is the program that starts a container
- runc is a common container runtime (compare it to systemd in linux)
- to manage a container that runs on a standalone computer, a container engine is used in top of container runtime
- docker and podman are the most common container engines for running standalone containers
- to run containers in cloud, kubernetes is used as the container engine
- as kubernetes is doing much more than just taking care of the running containers, it is called a container orchestrator

container_system/
├── image/
│   ├── definition/
│   │   ├── Dockerfile
│   │   ├── layers/
│   │   └── metadata.json
│   ├── stored_in/
│   │   ├── registry/
│   │   │   ├── dockerhub/
│   │   │   └── github_packages/
│   │   └── local_cache/
│   └── used_by/
│       ├── runtimes/
│       │   ├── runc/
│       │   └── crun/
│       └── orchestrators/
│           ├── kubernetes/
│           └── podman/
│
├── runtime/
│   ├── runc/
│   │   ├── responsibilities/
│   │   │   ├── create_container_namespace
│   │   │   ├── mount_filesystems
│   │   │   ├── isolate_processes
│   │   │   └── manage_lifecycle
│   │   └── communicates_with/
│   │       ├── docker/
│   │       ├── podman/
│   │       └── kubernetes/
│   └── alt_runtimes/
│       ├── crun/
│       ├── kata_containers/
│       └── gvisor/
│
├── platforms/
│   ├── docker/
│   │   ├── uses_runtime/ → runc
│   │   ├── builds_from/ → image
│   │   └── runs_on/ → computer | cloud
│   ├── podman/
│   │   ├── uses_runtime/ → runc
│   │   └── orchestrates/ → containers
│   ├── kubernetes/
│   │   ├── orchestrates/ → pods (containers)
│   │   └── uses_runtime/ → containerd → runc
│   └── cloud/
│       ├── aws_ecs/
│       ├── gcp_gke/
│       └── azure_aks/
│
└── environments/
    ├── computer/
    │   ├── linux/
    │   └── macos/
    └── cloud/
        ├── virtual_machines/
        ├── managed_clusters/
        └── serverless_containers/
