Morpheus Kubernetes Service (MKS) Clusters
------------------------------------------

Morpheus Kubernetes Service (MKS) is a CNCF-certified Kubernetes distribution that includes popular open source projects such as Calico, Prometheus and Grafana to quickly deploy a production ready Kubernetes cluster. MKS supports deployment on public clouds such as AWS, Azure, and GCP as well as on-premises hypervisors such as vSphere, Nutanix, and OpenStack.


Architecture
^^^^^^^^^^^^

.. image:: /images/infrastructure/clusters/mkeArchitecture.png


* Networking with Calico
* Monitoring with Prometheus
* Log forwarding with Fluentbit

**Supported Platforms:**

The Morpheus Kubernetes Service (MKS) distribution can be deployed on the following platforms:

* AWS
* GCP
* Nutanix
* VMware vSphere

**Packages:**

The folowing list of packages are included with a deployment of MKS.

* Calico
* Rook
* Fluentbit
* Prometheus
* Grafana

**Optional Packages:**

The following list of packages can be optionally added after deploying an MKS cluster.

* Istio
* Helm

Component Versions
^^^^^^^^^^^^^^^^^^^^^^^^^

This release of Morpheus Kubernetes Service (MKS) includes the following software component versions:

* containerd: 1.4.4
* calico: 3.17.2
* grafana: 7.3.4
* rook: 1.15
* prometheus: 2.22.1
* fluentbit: 1.7


Supported Operating Systems
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Morpheus Kubernetes Service (MKS) uses Ubuntu server as the operating system for control plane and worker nodes.


Firewall Ports
^^^^^^^^^^^^^^^^^^^^^

The Morpheus Kubernetes Service (MKS) cluster requires the following network ports:

.. list-table:: **Control Plane Node(s)**
  :widths: auto
  :header-rows: 1

  * - Protocol
    - Direction
    - Port Range
    - Purpose
    - Source
  * - TCP
    - Inbound
    - 2379-2380
    - etcd server client API
    - Self
  * - TCP
    - Inbound
    - 6443
    - Kubernetes API Server
    - All
  * - TCP
    - Inbound
    - 9100
    - Linux Node Exporter (Metrics)
    - Morpheus Platform
  * - TCP
    - Inbound
    - 10250
    - kubelet API
    - Self, Control plane
  * - TCP
    - Inbound
    - 10251
    - kube-scheduler
    - Self
  * - TCP
    - Inbound
    - 10252
    - kube-controller-manager
    - Self

.. list-table:: **Worker Node(s)**
  :widths: auto
  :header-rows: 1

  * - Protocol
    - Direction
    - Port Range
    - Purpose
    - Source
  * - TCP
    - Inbound
    - 9100
    - Linux Node Exporter (Metrics)
    - Morpheus Platform
  * - TCP
    - Inbound
    - 10250
    - kubelet API
    - Self, Control plane
  * - TCP
    - Inbound
    - 30000-32767
    - NodePort Services
    - All



Create an MKS Cluster
^^^^^^^^^^^^^^^^^^^^^

To create a new MKS Kubernetes Cluster:

#. Navigate to ``Infrastructure > Clusters``
#. Select :guilabel:`+ ADD CLUSTER`
#. Select ``Kubernetes Cluster``
#. Select a Group for the Cluster
#. Select :guilabel:`NEXT`
#. Populate the following:

   CLOUD
    Select target Cloud
   CLUSTER NAME
    Name for the Kubernetes Cluster
   RESOURCE NAME
    Name for Kubernetes Cluster resources
   DESCRIPTION
    Description of the Cluster
   VISIBILITY
    Public
      Available to all Tenants
    Private
      Available to Master Tenant
   LABELS
    Internal label(s)

#. Select :guilabel:`NEXT`
#. Populate the following:


Monitoring
^^^^^^^^^^

The performance of the Kubernetes cluster can be viewed


Access Grafana:

`
kubectl port-forward $(kubectl get pods -n monitoring -o name | grep grafana) 3000:3000 -n monitoring
`

Logging
^^^^^^^^^^

The performance of the Kubernetes cluster can be viewed


Access Prometheus: