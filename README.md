# OpenShift AI Model Deploy

This repository contains Kubernetes and OpenShift manifests for setting up an AI/ML platform on Red Hat OpenShift, with GPU support and model serving for large language models (LLMs). The configuration is organized as a reference deployment for enabling the OpenShift AI stack, NVIDIA GPU management, node feature discovery, model registry, and serving a sample model such as IBM Granite.

## Purpose

The goal of this project is to provide the YAML resources needed to:

- Install and configure the OpenShift AI / Data Science stack
- Enable NVIDIA GPU support on cluster nodes
- Expose hardware capabilities with Node Feature Discovery
- Deploy a model catalog and model registry
- Serve an inference model through KServe / OpenShift model deployment patterns

In practice, this repository is used as a deployment bundle for a GPU-enabled OpenShift cluster where AI workloads and inference endpoints can be exposed to users or applications.

## Repository structure

- `cm-time-slicing-config-all.yaml`: GPU time-slicing configuration for sharing a GPU between multiple workloads.

- `model-deploy/`: Deployment manifests for model serving, including:
  - service and route configuration
  - HPA and metrics configuration
  - kube-rbac-proxy and authentication-related config maps
  - secret and model deployment resources for the deployed model

- `model-registry/`: Configuration for the model catalog and model registry integration used by OpenShift AI.

- `node-feature-discovery-operator/`: Manifests for the OpenShift Node Feature Discovery operator, which labels nodes with hardware capabilities such as GPUs.

- `nvidia-gpu-operator/`: NVIDIA GPU Operator configuration, including the `ClusterPolicy` that defines driver, device plugin, runtime, and monitoring behavior for GPU workloads.

- `openshift-ai/`: OpenShift AI platform configuration, including:
  - `DataScienceCluster` setup
  - authentication configuration
  - gateway / hardware profile definitions
  - cluster initialization assets

## Typical deployment flow

The stack is meant to be applied in roughly this order:

1. Prepare the cluster with node discovery and GPU support.
2. Configure the OpenShift AI platform and data-science components.
3. Register model catalog and registry sources.
4. Deploy model-serving resources and expose the endpoint.

This repository is primarily infrastructure-as-code for an OpenShift AI environment rather than application code.

## Notes

The manifests reflect a Red Hat OpenShift environment with NVIDIA GPU acceleration and OpenShift AI services. The exact names, namespaces, and model identifiers may need to be adapted to your target cluster and deployment requirements.
