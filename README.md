# Scott Wares

Infrastructure and platform engineer in Littleton, Colorado. Two decades building the pipelines, secrets infrastructure, and monitoring that other engineers ship on — most recently as a Senior Principal Engineer at Raytheon, running platform services and observability for a secure software factory.

**Currently looking for** a senior platform, site reliability, or DevSecOps role. Denver metro or remote; permanent or contract.

waresscott@gmail.com · [LinkedIn](https://www.linkedin.com/in/scottwares/)

---

### What I'm building

Four repositories that form **one system**, not four standalone projects: a Kubernetes platform, its disposable cloud counterpart on AWS, an edge sensor and inference framework, and a network monitoring appliance — wired together through a shared device protocol, a containerized adapter, and a single GitOps deployment path.

**[HomeLab](https://github.com/swares/HomeLab)** — the platform

A three-node high-availability k3s cluster across a 14-host x86/ARM64 fleet. Argo CD reconciles everything from this repo with self-heal enabled, so change lands by pull request and rollback is a `git revert`. Ansible provisions the hosts, OpenTofu manages infrastructure with remote state in MinIO, and Renovate raises dependency PRs. HashiCorp Vault and External Secrets Operator handle the secrets path, cert-manager runs a private CA, Authelia and lldap provide OIDC single sign-on, and Kyverno enforces three cluster policies in Enforce mode. Observability is the full kube-prometheus-stack plus Loki and Alloy. An ARM64 inference tier runs behind a LiteLLM OpenAI-compatible gateway fronting Ollama, NPU-native RKLLama, and Whisper speech-to-text. [Read the case study →](https://github.com/swares/HomeLab/blob/main/docs/CASE-STUDY.md)

**[HomeLab-aws](https://github.com/swares/HomeLab-aws)** — the cloud tier

An Amazon EKS cluster built from nothing with OpenTofu, which bootstraps its own Argo CD, serves the AI gateway through an internet-facing ALB, and is destroyed every night at 02:00 by a least-privilege teardown job. A session costs about $1, against roughly $85 a month left running. Pods reach AWS through IRSA with no static keys, the teardown waits for controller-created load balancers *and* their network interfaces before destroying, and the budget alarm lives in a separate module so it outlives the thing it watches. It runs the same M5Stack adapter as the home lab, pulled from ECR, and it is deliberately detachable: the lab has a zero-line diff from it. [Read the case study →](https://github.com/swares/HomeLab-aws/blob/main/docs/CASE-STUDY.md)

**[M5Stack Sensor Framework](https://github.com/swares/My_M5Stack_Core_Framework)** — the edge tier

Auto-detects board family and I2C topology at runtime, so one binary runs across four M5Stack hardware families with no recompile. Plugin-per-device architecture, a threshold alarm engine with hysteresis and latching, and output routing to MQTT (with Home Assistant auto-discovery), webhooks, LCD, and SD. An on-device inference router classifies each request and dispatches it to a local NPU-hosted model, a cloud API, or an escalation path — keeping cheap requests local and reserving cloud calls for work that needs them. Its host-side adapter is containerized and deployed into the cluster as an OpenAI-compatible backend behind the LiteLLM gateway, which makes the edge hardware a first-class inference backend rather than a side project.

**[HostMon](https://github.com/swares/HostMon)** — the monitoring appliance

Firmware for the Waveshare ESP32-S3, running six check types (ICMP, DNS, TCP, HTTP/S, TLS certificate expiry, traceroute) with an embedded web dashboard, a JSON REST API, and webhook alerting with debounce, re-notify, and acknowledge/pause governance. Alerts post over an authenticated webhook straight into the M5Stack device's alert engine — no relay in between. Hardened with per-device random credentials compared in constant time, CSRF origin validation, and server-side input validation, and it ships with a threat model documenting what it *doesn't* protect against and the hardware reasons why.

**Where the seams are.** The repositories split on coupling, not convenience: code bound to the firmware protocol lives with the firmware behind one shared protocol client, so a protocol change is a single commit across firmware and both consumers. Deployment manifests stay in the GitOps repo, and images publish to a private registry and reach the cluster by pinned tag through Argo CD.

---

### What I work with

**Platform** Kubernetes · Argo CD · Helm · Docker · containerd · Terraform / OpenTofu · Ansible · Puppet · Packer

**CI/CD** Jenkins & CloudBees (configuration as code, shared libraries) · GitLab CI · JFrog Artifactory · Git

**Observability** Prometheus · Grafana · Alertmanager · Loki · OpenTelemetry · ELK · Splunk · Nagios / Icinga2

**Security** HashiCorp Vault · PKI and certificate authority design · Kyverno · cert-manager · Authelia / OIDC · LDAP

**Cloud & systems** AWS · OpenStack · vSphere · KVM · RHEL · Ubuntu · Debian · SUSE · Solaris

**Languages** Python · Bash · Perl · Groovy · PowerShell · C / C++
