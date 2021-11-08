Morpheus Kubernetes Service (MKS) Clusters
------------------------------------------

Morpheus Kubernetes Service (MKS) is a CNCF-certified Kubernetes distribution that supports deployment on public clouds such as AWS, Azure, and GCP as well as on-premises hypervisors such as vSphere, Nutanix, and OpenStack. Morpheus Kubernetes Service (MKS) provides a simple and easy way to deploy a Kubernetes cluster through the Morpheus platform.

Features
^^^^^^^^

* CNCF Certified Distribution

Architecture
^^^^^^^^^^^^

.. image:: /images/infrastructure/clusters/mkeArchitecture.png

**Packages**

The folowing list of packages are included with a deployment of MKS:

* **Calico:** Calico Open Source is a networking and security solution for containers, virtual machines, and native host-based workloads. It supports a broad range of platforms including Kubernetes, OpenShift, Docker EE, OpenStack, and bare metal services.
* **Rook:** Rook is an open source cloud-native storage orchestrator, providing the platform, framework, and support for a diverse set of storage solutions to natively integrate with cloud-native environments.
* **Fluentbit:** Fluent Bit is an open source Log Processor and Forwarder which allows you to collect any data like metrics and logs from different sources, enrich them with filters and send them to multiple destinations.
* **Prometheus:** Prometheus is an open-source systems monitoring and alerting toolkit.
* **Grafana:** Grafana is a multi-platform open source analytics and interactive visualization web application.

**Optional Packages**

The following list of packages can be optionally added after deploying an MKS cluster:

* **Istio:** Istio is an open platform-independent service mesh that provides traffic management, policy enforcement, and telemetry collection.
* **Helm:** Helm is the package manager for Kubernetes that simplifies the installation and ugprade of software running on Kubernetes.

Supported Platforms
^^^^^^^^^^^^^^^^^^^

The Morpheus Kubernetes Service (MKS) distribution can be deployed on the following platforms:

* AWS
* GCP
* Nutanix
* VMware vSphere

Supported Operating Systems
^^^^^^^^^^^^^^^^^^^^^^^^^^^
Morpheus Kubernetes Service (MKS) uses Ubuntu server as the operating system for control plane and worker nodes.

Component Versions
^^^^^^^^^^^^^^^^^^^^^^^^^

This release of Morpheus Kubernetes Service (MKS) includes the following software component versions:

* containerd: 1.4.4
* calico: 3.17.2
* grafana: 7.3.4
* rook: 1.15
* prometheus: 2.22.1
* fluentbit: 1.7

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

Create an MKS Cluster on VMware vSphere
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

To create a new MKS Kubernetes Cluster:


.. tabs::

    .. tab:: Morpheus UI

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


    .. tab:: CLI


    .. tab:: API


Monitoring
^^^^^^^^^^

In addition to the built-in cluster and workload monitoring the MKS cluster also provides access to the Prometheus, Alertmanager and Grafana web interfaces.

**Grafana**

Grafana allows you to visualize the performance metrics of the Kubernetes cluster. Several Kubernetes dashboards are included to quickly view detailed metrics from Prometheus. 

#. Run the following command to port forward the local grafana dashboard

.. code-block:: bash

    kubectl port-forward svc/grafana 3000:3000 -n monitoring

#. Open the following address in the web browser: http://localhost:3000

Username: admin
Password: admin


**Prometheus**

.. code-block:: bash

    kubectl port-forward svc/prometheus-k8s -n monitoring 9090:9090

#. Open the following address in the web browser: http://localhost:9090

**Alertmanager**

.. code-block:: bash

    kubectl port-forward svc/alertmanager-main -n monitoring 9093:9093

#. Open the following address in the web browser: http://localhost:9093

Logging
^^^^^^^

The performance of the Kubernetes cluster can be viewed

Delete MKS Cluster
^^^^^^^^^^^^^^^^^^

When you're done using a Kubernetes cluster you can delete the cluster using the Morpheus user interface, the Morpheus API or the Morpheus CLI.

**To delete a Kubernetes cluster with the Morpheus UI**

1. Select **Clusters** from the **Infrastructure** tab drop-down menu
2. Click on the trash can to the right of the Kubernetes cluster that you want to delete
3. Type **DELETE** in the text box to confirm that you want to delete the Kubernetes cluster and click **DELETE** to destroy the Kubernetes cluster.

**To delete a Kubernetes cluster with the Morpheus CLI**

1. List all the Kubernetes clusters

   ```bash
   morpheus clusters list
   ```

   The ID of the cluster is required to delete the Kubernetes cluster.

   ```bash
   Morpheus Clusters
   ==================
   ID | NAME     | TYPE
   ---|----------|-------------------
   25 | k3s      | Kubernetes Cluster
   24 | kubedemo | Kubernetes Cluster
   ```

2. Delete the Kubernetes cluster using the ID identified in the previous step.

   ```bash
   morpheus clusters remove <cluster-id>
   ```

   Confirm that you want to delete the Kubernetes cluster by entering **yes** when prompted if you would like to remove the cluster.

   ```bash
   Are you sure you would like to remove the cluster <cluster-name>? (yes/no): yes
   ```

   The cluster may take a few moments to be completely removed.

   ```bash
   Cluster <cluster-name> is being removed...
   ```

**To delete a Kubernetes cluster with the Morpheus API (CURL)**

1. List all the Kubernetes clusters

   ```bash
   curl 
   ```

2. T
