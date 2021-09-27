Morpheus Kubernetes Service (MKS) Clusters
------------------------------------------

Morpheus Kubernetes Service (MKS) is a CNCF-certified Kubernetes distribution that includes popular open source projects such as Calico, Prometheus and Grafana to quickly deploy a production ready Kubernetes cluster. MKS supports deployment on public clouds such as AWS, Azure, and GCP as well as on-premises hypervisors such as vSphere, Nutanix, and OpenStack.


Firewall Ports
^^^^^^^^^^^^^^^^^^^^^

.. list-table:: **Control-plane node(s)**
  :widths: auto
  :header-rows: 1

  * - Protocol
    - Direction
    - Port Range
    - Purpose
    - Used By
  * - TCP
    - Inbound
    - 6443
    - Kubernetes API Server
    - All
  * - TCP
    - Inbound
    - 6783
    - Weaveworks
    - 
  * - TCP
    - Inbound
    - 2379-2380
    - etcd server client API
    - kube-apiserver, etcd
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

.. list-table:: **Worker node(s)**
  :widths: auto
  :header-rows: 1

  * - Protocol
    - Direction
    - Port Range
    - Purpose
    - Source
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