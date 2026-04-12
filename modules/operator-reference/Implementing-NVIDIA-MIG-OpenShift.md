# Implementing NVIDIA MIG in Red Hat OpenShift to optimize GPU resources in containerized environments

## Temperature

Use this data to identify bottlenecks and optimize MIG configurations for better performance. By analyzing these metrics over time, you can make informed decisions about resource allocation and identify opportunities for further optimization.

## Automated scaling

Implement auto-scaling policies based on GPU utilization metrics to ensure efficient resource allocation:

- Scale up MIG instances when utilization consistently exceeds 80%
- Scale down or reconfigure when utilization drops below 20%

This approach ensures that GPU resources are always optimally allocated, improving overall cluster efficiency and reducing costs.

## Advanced MIG configurations

Finally, consider these advanced MIG configurations:

- Heterogeneous MIG setups
- Integration with OpenShift virtualization

### Heterogeneous MIG setups

For maximum flexibility, consider using the 'mixed' MIG strategy, which allows for diverse MIG configurations across different GPUs:

```yaml
spec:
  mig:
    strategy: mixed
    config:
```

---

**Was this content helpful?**

---

**Source:** IBM Developer

---

## About cookies on this site

Our websites require some cookies to function properly (required). In addition, other cookies may be used with your consent to analyze site usage, improve the user experience and for advertising.

For more information, please review your cookie preferences options. By visiting our website, you agree to our processing of information as described in IBM's privacy statement.

To provide a smooth navigation, your cookie preferences will be shared across the IBM web domains listed here.
