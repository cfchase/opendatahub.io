---
layout: docs
title: Quick Installation(v2)
permalink: /docs/getting-started/quick-installation-new-operator
style_class: quick-installation
---
## disclaimer

Version 2.X represents an alpha release, exclusively accessible via the "fast" channel.
Subsequent releases will transition to the "fast" channel once the new operator attains greater stability.

For installation steps of the old (version 1.X, stable),
see [quick installation of the 1.X version](../quick-installation).

### Pre-requisites

Below information is only appliable for Open Data Hub Operator v2.0.0 and forth release.

Installing Open Data Hub requires OpenShift Container Platform version 4.10+.
All screenshots and instructions are from OpenShift 4.12.
For the purposes of this quick start, we used [try.openshift.com](https://try.openshift.com/) on AWS.

Tutorials will require an OpenShift cluster with a minimum of 16 CPUS and 32GB of memory across all OpenShift worker nodes.

### Installing the New Open Data Hub Operator

The Open Data Hub operator is available for deployment in the OpenShift OperatorHub as a Community Operator. You can install it from the OpenShift web console by following the steps below:

1. From the OpenShift web console, log in as a user with `cluster-admin` privileges.  For a developer installation from [try.openshift.com](https://try.openshift.com/), the `kubeadmin` user will work.
   ![Log in to OpenShift](../assets/img/pages/docs/quick-installation/login.png)

2. On the lefthand bar, from `Operators` -> `OperatorHub`,
   - filter for `Open Data Hub Operator`.
   - select `AI/Machine Learning` and look for the icon for `Open Data Hub Operator`.
   ![OperatorHub](../assets/img/pages/docs/quick-installation-new-operator/operator-hub.png "OperatorHub")

3. Click `Continue` in the "Show community Operator" dialog if it pops out. Click the `Install` button to install the Open Data Hub operator.
   ![Install](../assets/img/pages/docs/quick-installation-new-operator/installation1.png "Install")

4. The subscription creation view will offer a few options including `Update Channel`, make sure the `fast` channel is selected. Click `Install` to deploy the opendatahub operator into the `openshift-operators` namespace.
   ![Select Channel](../assets/img/pages/docs/quick-installation-new-operator/channels.png "Select Channel")

5. To view the status of the Open Data Hub operator installation, find the Open Data Hub Operator under `Operators` -> `Installed Operators`. It might take a couple of minutes to show, but once the `Status` field displays `Succeeded`, you can proceed to create a DataScienceCluster instance
   ![Installed Operators](../assets/img/pages/docs/quick-installation-new-operator/operator-installed.png "Installed Operators")

### Create a DataScienceCluster instance

1. Click on the `Open Data Hub Operator` from `Installed Operators` page to bring up the details for the version that is currently installed.
   ![Open Data Hub Operator](../assets/img/pages/docs/quick-installation-new-operator/odh-operator.png "Open Data Hub Operator")

2. Two ways to create DataScienceCluster instance:
   - Click `Create DataScienceCluster` button from the top warning dialog `DataScienceCluster required(Create a DataScienceCluster instance to use this Operator.)`
   - Click tab `Data Science Cluster` then click `Create DataScienceCluster` button

   They both lead to a new view called "Create DataScienceCluster". By default, namespace/project `opendatahub` is used to host all applications.

3. In the view of "Create DataScienceCluster", user can create DataScienceCluster instance in two ways with `components` fields.
   - Form view:
      a. Fill in `Name` field
      b. In the `components` section, click `>` to expand the list of currently supported core components. Check the set of components enabled by default and tick/untick the box in each component section to tailor the selection.
      ![Create DSC2](../assets/img/pages/docs/quick-installation-new-operator/create-dsc-component1.png "Create DSC2")

   - YAML view:
      a. View the detail schema by expanding the right-hand sidebar ![Create DSC1](../assets/img/pages/docs/quick-installation-new-operator/create-dsc-component2.png "Create DSC1")
      b. Read [ODH Core components](../tiered-components) to get the full list of supported components.

4. Click `Create` button to finalize creation process in seconds.
   ![DSC Status](../assets/img/pages/docs/quick-installation-new-operator/dsc-installed.png "DSC Status")

5. Verify the installation by viewing the project workload.
   Click `Home` then `Projects`, select "opendatahub" project, in the `Workloads` tab to view enabled compoenents. These should be running.
   ![Verify Status](../assets/img/pages/docs/quick-installation-new-operator/verify-install.png "Verify Status")

### Open Data Hub Dashboard

The data scientists and other users will most likely use the
Open Data Hub features through Open Data Hub Dashboard. Its URL can be
found in Menu > Networking > Routes, Project `opendatahub`,
the Location colum of the `odh-dashboard` route.

### Dependencies

- to use "kserve" component, users are required to install two operators via OperatorHub before enable it in DataScienceCluster CR
   1. Red Hat OpenShift Serverless Operator from "Red Hat" catalog.
   2. Red Hat OpenShift Service Mesh Operator from "Red Hat" catalog.

- to use "kserve" component, with authentication, user need to install Authorino oprator via OperatorHub before create DSCI CR
   1. Authorino Operator from "Red Hat" catalog.

- to use "datasciencepipeline" component, users are required to install one operator via OperatorHub before enable it in DataScienceCluster CR
   1. Red Hat OpenShift Pipelines Operator from "Red Hat" catalog.

- to use "distributedworkloads" component, users are required to install one operator via OperatorHub before enable it in DataScienceCluster CR
   1. CodeFlare Operator from "Community" catalog.

- to use "modelmesh" component, users are required to install one operator via OperatorHub before enable it in DataScienceCluster CR
   1. Prometheus Operator from "Community" catalog.
