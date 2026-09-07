# Scott Wares

Infrastructure and platform engineer in Littleton, Colorado. Two decades building the pipelines, secrets infrastructure, and monitoring that other engineers ship on — most recently as a Senior Principal Engineer at Raytheon, running platform services and observability for a secure software factory.

**Currently looking for** a senior platform, site reliability, or DevSecOps role. Denver metro or remote; permanent or contract.

waresscott@gmail.com · [LinkedIn](https://www.linkedin.com/in/scottwares/)

---

### What I'm building

**[HomeLab](https://github.com/swares/HomeLab)** — a GitOps-managed Kubernetes platform

A three-node high-availability k3s cluster across a 14-host x86/ARM64 fleet. Argo CD reconciles everything from this repo with self-heal enabled, so change lands by pull request and rollback is a `git revert`. Ansible provisions the hosts, OpenTofu manages infrastructure with remote state in MinIO, and Renovate raises dependency PRs. HashiCorp Vault and External Secrets Operator handle the secrets path, cert-manager runs a private CA, Authelia and lldap provide OIDC single sign-on, and Kyverno enforces three cluster policies in Enforce mode. Observability is the full kube-prometheus-stack plus Loki and Alloy. There's also an ARM64 inference tier — a LiteLLM OpenAI-compatible gateway fronting Ollama and NPU-native RKLLama, with Whisper for speech-to-text.

**[HostMon](https://github.com/swares/HostMon)** — a network monitoring appliance in C++

Firmware for the Waveshare ESP32-S3, running six check types (ICMP, DNS, TCP, HTTP/S, TLS certificate expiry, traceroute) with an embedded web dashboard, a JSON REST API, and webhook alerting with debounce, re-notify, and acknowledge/pause governance. Hardened with per-device random credentials compared in constant time, CSRF origin validation, and server-side input validation. Ships with a threat model that documents what it *doesn't* protect against, and the hardware reason why.

**[M5Stack Sensor Framework](https://github.com/swares/My_M5Stack_Core_Framework)** — a plugin framework for I2C sensors

Auto-detects board family and I2C topology at runtime, so one binary runs across four M5Stack hardware families with no recompile. Plugin-per-device architecture, a threshold alarm engine with hysteresis and latching, and output routing to MQTT (with Home Assistant auto-discovery), webhooks, LCD, and SD. Includes an on-device inference router that classifies each request and dispatches it to a local NPU-hosted model, a cloud API, or an escalation path — keeping cheap requests local and reserving cloud calls for work that needs them.

---

### What I work with

**Platform** Kubernetes · Argo CD · Helm · Docker · containerd · Terraform / OpenTofu · Ansible · Puppet · Packer

**CI/CD** Jenkins & CloudBees (configuration as code, shared libraries) · GitLab CI · JFrog Artifactory · Git

**Observability** Prometheus · Grafana · Alertmanager · Loki · OpenTelemetry · ELK · Splunk · Nagios / Icinga2

**Security** HashiCorp Vault · PKI and certificate authority design · Kyverno · cert-manager · Authelia / OIDC · LDAP

**Cloud & systems** AWS · OpenStack · vSphere · KVM · RHEL · Ubuntu · Debian · SUSE · Solaris

**Languages** Python · Bash · Perl · Groovy · PowerShell · C / C++
