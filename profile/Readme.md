# Charité Virtual Research Environment (VRE) AutoDeploy

Copyright (c) Charité – Universitätsmedizin Berlin

[![License](https://img.shields.io/badge/License-EUPL%20v1.2-blue.svg)](https://joinup.ec.europa.eu/collection/eupl/eupl-text-eupl-12)
[![Kubernetes](https://img.shields.io/badge/Kubernetes-≤1.29.x-326ce5.svg)](https://kubernetes.io/)
[![Terraform](https://img.shields.io/badge/Terraform-v1.10+-623CE4.svg)](https://terraform.io/)
[![Helm](https://img.shields.io/badge/Helm-v3.17+-0F1689.svg)](https://helm.sh/)

Welcome to the **Charité Virtual Research Environment (VRE) AutoDeploy** organization - your gateway to automated, GDPR-compliant digital research infrastructure.

## 🚀 What is the VRE?

The Virtual Research Environment is a secure, cloud-native, **GDPR-compliant digital research platform** designed to empower researchers with secure, scalable, and collaborative tools for modern scientific discovery. Built with privacy-by-design principles, VRE provides a comprehensive ecosystem where sensitive research data can be processed, analyzed, and shared while maintaining the highest standards of data protection and regulatory compliance. This repository collection provides infrastructure-as-code automation with Terraform and Helm Charts, enabling rapid, scalable, and reproducible deployment of the GDPR-compliant VRE ecosystem on Kubernetes.
Built to meet the strict requirements of GDPR and FAIR data principles, it empowers researchers with compliant, modular, and scalable digital tools to manage, process, and share sensitive health data.

VRE is a node of the [EBRAINS Health Data Cloud](https://www.ebrains.eu/tools/healthdatacloud) and supports a wide range of neuroscience initiatives and clinical research across Europe.

### 🎯 Key Features

- **🔒 GDPR Compliance**: Built-in privacy controls and data protection mechanisms
- **☁️ Cloud-Native Architecture**: Kubernetes-based for scalability and resilience as well as Kong, Keycloak, Elasticsearch, MinIO, Neo4j, OpenLDAP, cert-manager, Jaeger, and more.
- **🔄 Automated Deployment**: One-click infrastructure provisioning with Terraform and Helm
- **🔐 Enterprise Security**: Multi-layered authentication and authorization systems
- **📊 Comprehensive Analytics**: Integrated observability and monitoring stack
- **🤝 Collaborative Workspace**: Secure data sharing and team collaboration tools


## 🛠️ AutoDeploy Architecture

This new **AutoDeploy version** revolutionizes VRE deployment through complete automation:

### Infrastructure as Code
- **Terraform**: Automated provisioning and configuration managements – Declarative Terraform templates for each deployment phase (pre-install, install, intermediary-install, post-install).
- **Helm Charts**: Streamlined Kubernetes application deployment – Modular Kubernetes application packages for VRE components.
- **GitOps Workflow**: Version-controlled infrastructure changes
- **Secrets & Configuration Guidance**: Clearly structured guidance for secure deployment setup.
- **Scalable Environments**: Easily configure new staging or production environments using customizable .tfvars files.

### Core Components
- **Identity & Access Management**: Keycloak-based authentication with LDAP integration
- **Data Management**: MinIO object storage with encryption at rest
- **Service Mesh**: Kong API gateway for secure service communication  
- **Observability Stack**: Elasticsearch, monitoring, and distributed tracing
- **Database Layer**: Neo4j graph database and Redis caching
- **Certificate Management**: Automated TLS certificate provisioning

## 🚀 Quick Start

### Prerequisites
- Kubernetes cluster (≤ 1.29.x)
- Storage provider with RWO/RWX support
- LoadBalancer capability

### One-Command Deployment
```bash
# Clone the repository
git clone https://github.com/vre-charite-autodeploy/vre-infra.git
cd vre-infra

# Configure your environment
cp ./terraform/config/charite/charite.tfvars ./terraform/config/production/production.tfvars
vi ./terraform/config/production/production.tfvars

# Deploy VRE
export TF_VAR_ghcr_token="username:token"
export TF_VAR_kubeconfig="/path/to/kubeconfig"

# Automated deployment across all stages
FOLDERS=("pre-install" "install" "intermediary-install" "post-install")
for TF_FOLDER in "${FOLDERS[@]}"; do
  terraform -chdir=./terraform/${TF_FOLDER} init
  terraform -chdir=./terraform/${TF_FOLDER} apply --auto-approve -var-file=../config/production/production.tfvars
done
```

👉 Read the full deployment guide in [vre-infra repository](https://github.com/vre-charite-autodeploy/vre-infra) for detailed steps.


## 📚 Documentation & Resources

- **📖 [Deployment Guide](https://github.com/vre-charite-autodeploy/vre-infra/blob/main/DEPLOYMENT.md)**: Complete step-by-step deployment instructions
- **🔧 [Configuration Reference](https://github.com/vre-charite-autodeploy/vre-infra/tree/main/terraform/config)**: Detailed configuration options
- **💬 [Community Support](https://github.com/vre-charite-autodeploy/discussions)**: <vre-support@charite.de> and [register for our bi-weekly community meetings](https://us06web.zoom.us/meeting/register/tJErd-utqzkpHtI9rpX8cJVNSidRbM5wuMe1?_x_zm_rtaid=IJCTpcS4SGOCk1TKSMrfZQ.1747903776635.dde5dddf0170eaf75f6b4b29162b6480&_x_zm_rhtaid=232#/registration).

## 🌟 Use Cases

- **Clinical Research**: Secure processing of patient data with GDPR compliance
- **Biomedical Analytics**: Large-scale genomics and proteomics analysis
- **Multi-Center Studies**: Collaborative research across institutions
- **AI/ML Workflows**: Scalable machine learning pipeline execution
- **Data Harmonization**: Standardized data processing and integration

## 🏆 Recognition & Impact

The VRE has been adopted across leading research institutions and is actively contributing to breakthrough discoveries in neuroscience, digital health, and computational biology. Our GDPR-compliant approach has become a reference implementation for research data management in Europe.

## 🤝 Contributing

We welcome contributions from the research and developer community! Whether you're fixing bugs, adding features, or improving documentation, your input helps make VRE better for everyone.

- **🐛 Report Issues**: Found a bug? Let us know!
- **💡 Feature Requests**: Have an idea? We'd love to hear it!
- **🔧 Pull Requests**: Ready to contribute code? Submit a PR!
- **📖 Documentation**: Help improve our guides and tutorials

## 📄 License

This project is licensed under the European Union Public License v1.2 - see the [LICENSE](https://github.com/vre-charite-autodeploy/vre-infra/blob/main/LICENSE) file for details.

---

## 🙏 Acknowledgments

This work is proudly supported by a consortium of leading European research initiatives and institutions:

**European Union Programs:**
- EU Horizon Europe program Horizon EBRAINS2.0 (101147319)
- Virtual Brain Twin (101137289)
- EBRAINS-PREP (101079717)
- AISN (101057655)
- EBRAIN-Health (101058516)
- EIC grant PHRASE (101058240)

**Digital Europe Programme:**
- TEF-Health (101100700)
- Shaiped (101195135)
- CoordinaTEF (101168074)

**German Research Foundation (DFG):**
- SFB 1436 (project ID 425899996)
- SFB 1315 (project ID 327654276)
- SFB 936 (project ID 178316478)
- SFB-TRR 295 (project ID 424778381)
- SPP Computational Connectomics RI 2073/6-1, RI 2073/10-2, RI 2073/9-1
- DFG Clinical Research Group BECAUSE-Y 504745852

**Institutional Partners:**
- Berlin University Alliance OpenMake
- Virtual Research Environment at the Charité Berlin
- EBRAINS Health Data Cloud
- Berlin Institute of Health and Foundation Charité
- de.NBI cloud

---

<div align="center">

**🔬 Empowering Research Through Secure, Compliant, and Scalable Digital Infrastructure 🔬**

[Get Started](https://github.com/vre-charite-dev/vre-infra) • [Documentation](https://github.com/vre-charite-autodeploy) • [Community](https://us06web.zoom.us/meeting/register/tJErd-utqzkpHtI9rpX8cJVNSidRbM5wuMe1?_x_zm_rtaid=IJCTpcS4SGOCk1TKSMrfZQ.1747903776635.dde5dddf0170eaf75f6b4b29162b6480&_x_zm_rhtaid=232#/registration)

</div>
