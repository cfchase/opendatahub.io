---
layout: docs
title: Quick Installation(v1)
permalink: /docs/getting-started/quick-installation
style_class: quick-installation
---

This document describes installation steps for the version 1.X (old) operator.
For installation steps of the new (version 2.X, alpha),
see [quick installation of the new operator](../quick-installation-new-operator).

### Pre-requisites

Installing Open Data Hub requires OpenShift Container Platform version 4.10+. All screenshots and instructions are from OpenShift 4.10.  For the purposes of this quick start, we used [try.openshift.com](https://try.openshift.com/) on AWS.  Tutorials will require an OpenShift cluster with a minimum of 16 CPUS and 32GB of memory across all OpenShift worker nodes.

### Installing the Open Data Hub Operator

The Open Data Hub operator is available for deployment in the OpenShift OperatorHub as a Community Operator. You can install it from the OpenShift web console by following the steps below:

1. From the OpenShift web console, log in as a user with `cluster-admin` privileges.  For a developer installation from [try.openshift.com](https://try.openshift.com/), the `kubeadmin` user will work.
   ![Log in to OpenShift](../assets/img/pages/docs/quick-installation/login.png)

1. Find `Open Data Hub` in the `OperatorHub` catalog.
   1. Under `Operators`, select `OperatorHub` for a list of operators available for deployment.
   1. Filter for `Open Data Hub` or look under `AI/Machine Learning` for the icon for `Open Data Hub`.
   ![OperatorHub](../assets/img/pages/docs/quick-installation/operator-hub.png "OperatorHub")

1. Click the `Install` button and follow the installation instructions to install the Open Data Hub operator.
   ![Install](../assets/img/pages/docs/quick-installation/install.png "Install")

1. The subscription creation view will offer a few options including *Update Channel*, 
   keep the `rolling` channel selected. Click `Install` to deploy the opendatahub operator into the `openshift-operators` namespace.
   ![Select Channel](../assets/img/pages/docs/quick-installation/channels.png "Install")

1. Click `View Operator` to navigate to the OpenShift OperatorHub page for the newly install ODH operator.
   ![View Operator](../assets/img/pages/docs/quick-installation/installed-operator-ready-for-use.png "View Installed ODH Operator")

1. To view the status of the Open Data Hub operator installation, find the Open Data Hub Operator under `Operators` -> `Installed Operators`. Once the STATUS field displays `Succeeded`, you can proceed to create a new Open Data Hub deployment.
   ![Installed Operators](../assets/img/pages/docs/quick-installation/installed-operators.png "Installed Operators")

1. Create a new namespace named `odh` for your installation of Open Data Hub.
   ![Create Namespace 'odh'](../assets/img/pages/docs/quick-installation/create-namespace.png "Create Namespace 'odh'")

1. Select the new `odh` namespace if not already selected.

### Create a New Open Data Hub Deployment

The Open Data Hub operator will create new Open Data Hub deployments and manage its components.  Let's create a new Open Data Hub deployment.

1. Find the Open Data Hub Operator under `Installed Operators` (inside the namespace you created earlier)
   ![Installed Operators](../assets/img/pages/docs/quick-installation/installed-operators.png "Installed Operators")

1. Click on the Open Data Hub Operator to bring up the details for the version that is currently installed.
   ![Open Data Hub Operator](../assets/img/pages/docs/quick-installation/odh-operator.png "Open Data Hub Operator")

1. Click `Create Instance` for `KfDef` to create a new deployment.  The default `kfdef` provided will deploy the latest release of the [ODH Core components](../tiered-components). If you accepted the default name, this will trigger the creation of an Open Data Hub kfdef object named `opendatahub` and start the rollout of the [ODH Core components](../tiered-components).
   ![Create New ODH](../assets/img/pages/docs/quick-installation/new-deployment.png "Create New ODH")

1. Verify the installation by viewing the Open Data Hub tab within the operator details.  You Should see `opendatahub` listed.
   ![ODH List](../assets/img/pages/docs/quick-installation/odh-list.png "ODH List")

1. Verify the installation by viewing the project workload.  The [ODH Core components](../tiered-components) should be running.
   ![Verify Status](../assets/img/pages/docs/quick-installation/verify-install.png "Verify Status")

   If you Create an Instance that is not under `odh` a fatal error similar to "csv created in namespace with multiple operatorgroups, can't pick one automatically" will be raised.
   ![Change Namespace to 'odh'](../assets/img/pages/docs/quick-installation/installed-operators-change-namespace.png "Change Namespace to 'odh'")

### Open Data Hub Dashboard

The data scientists and other users will most likely use the
Open Data Hub features through Open Data Hub Dashboard. Its URL can be
found in Menu > Networking > Routes, Project `odh`,
the Location colum of the `odh-dashboard` route.

### Upgrade to new operator(version 2.X)

If you are currently having version 1.X installed and prefer upgrading to new operator 2.X, please follow below instruction:

- Login from the OpenShift web console with `cluster-admin` privileges
- Go to `Operator` -> `Installed Operators`, choose `Open Data Hub Operator` which is on 1.X version.
- Click `Subscription` tab
- In the `Update channel` section, you should see `rolling` as the current channel.
![change channel](../assets/img/pages/docs/quick-installation/change-channel.png "change channel")

- Click `pencil` icon next to `rolling`, in the popup window `Change Subscription update channel`, tick `fast` icon, then `Save` your option.
- If you have `Update approval` already configed to `Automatic`, you should see `Upgrade status` change to `1 installing` in minutes.
- The rest steps, please refer to [here from step 5](../quick-installation-new-operator#installing-the-new-open-data-hub-operator)

#### disclaimer

1. Version 2.X represents an alpha release, exclusively accessible via the "fast" channel.

Subsequent releases will transition to the "rolling" channel once the new operator attains greater stability.

2. During the installation of the new operator (v2.X), applications will not be automatically updated from v1.X to v2.X.

Users will need to create a DataScienceCluster instance and enable specific components based on their requirements.

3. If the current application namespace for v1.X is not "opendatahub", users must scale down the components first.
