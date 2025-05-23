# k8ops - Kubernetes Operations Tools

[![Publish Python Package to PyPI](https://github.com/nomagicln/k8ops/actions/workflows/publish-to-pypi.yml/badge.svg?branch=main)](https://github.com/nomagicln/k8ops/actions/workflows/publish-to-pypi.yml)

A collection of tools to help with Kubernetes cluster operations and management.

## Installation

You can install k8ops using pip:

```bash
pip install k8ops
```

Or using uv:

```bash
uv pip install k8ops
```

## Requirements

- Python 3.7+
- `kubectl` configured with access to your Kubernetes cluster

## Features

### Node Summary

The node summary command provides detailed information about cluster nodes:

```bash
k8ops cluster summary [options] [node_names...]
```

#### Options

- `--wide`: Show wide output with additional columns
- `--pods`: Show pods running on each node
- `--images`: Show container images on each node
- `--taints`: Show node taints
- `--labels`: Show node labels
- `--annotations`: Show node annotations
- `--capacity`: Show node capacity
- `--allocatable`: Show node allocatable resources
- `--conditions`: Show node conditions
- `--addresses`: Show node addresses
- `--metrics`: Show node metrics
- `--all`: Show all information

### Node Drain Analyzer

The node drain analyzer helps assess the impact and risks of draining nodes from your Kubernetes cluster:

```bash
k8ops cluster drain [options] <node_names...>
```

#### Features

- Comprehensive drain impact analysis:
  - Resource usage evaluation (CPU, memory, pods)
  - Pod scheduling constraints check
  - Architecture and OS compatibility verification
  - Taint and toleration validation
  - DaemonSet impact assessment
  - Running jobs/cronjobs detection
  - Node selector and affinity rules check
  - Resource availability calculation

#### Options

All options from the summary command are supported, plus:

- `--factor`: The factor for resource calculations when pods have no requests set (default: 1.5)

#### Analysis Details

The analyzer checks for various potential issues:

1. **Resource Constraints**
   - CPU and memory availability on remaining nodes
   - Pod capacity limits
   - Resource distribution impact

2. **Scheduling Constraints**
   - Node selectors compatibility
   - Affinity/anti-affinity rules
   - Taints and tolerations
   - Architecture/OS compatibility

3. **Workload Impact**
   - DaemonSet pods
   - Running jobs/cronjobs
   - Pods with no controllers
   - Pod density changes

#### Severity Levels

- **High**: Critical issues that will likely prevent successful node draining
- **Medium**: Significant issues that may cause problems
- **Low**: Minor issues that should be reviewed
- **None**: No issues detected

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

[MIT License](LICENSE)
