---
author_name: Iwona Hahn
author_profile: https://github.com/iwonahahn
title: Prepare for SAP BTP Development
description: Learn how to prepare SAP BTP and Kyma for application deployment.
keywords: cap
auto_validation: true
time: 25
tags: [ tutorial>beginner, software-product-function>sap-cloud-application-programming-model, programming-tool>node-js, software-product>sap-business-technology-platform, software-product>sap-btp-kyma-runtime, software-product>sap-fiori]
primary_tag: software-product-function>sap-cloud-application-programming-model
---

## Prerequisites
 - [Set Up Local Development using VS Code](btp-app-set-up-local-development)
 - [Create a Directory for Development](btp-app-create-directory)
 - [Create a CAP-Based Application](btp-app-create-cap-application)
 - [Create an SAP Fiori Elements-Based UI](btp-app-create-ui-fiori-elements)
 - [Add Business Logic to Your Application](btp-app-cap-business-logic)
 - [Create a UI Using Freestyle SAPUI5](btp-app-create-ui-freestyle-sapui5)
 - [Use a Local Launch Page](btp-app-launchpage)
 - [Implement Roles and Authorization Checks in CAP](btp-app-cap-roles)

## Details
### You will learn
 - How to create an account for SAP BTP
 - How to assign entitlements
 - How to configure Kyma in your SAP BTP subaccount


---

[ACCORDION-BEGIN [Step 1: ](Overview)]
> ### To earn your badge for the whole mission, you will need to mark all steps in a tutorial as done, including any optional ones that you may have skipped because they are not relevant for you.

You need an SAP BTP account to deploy the services and applications.
In general, you have a choice of the following options:

**Trial:** *(recommended)* Use a trial account if you just want to try out things and don't want to use any of the parts of this tutorial productively. The usage is free of cost and all the services that you need for this tutorial get automatically assigned to your trial account.

> When running the tutorial with a trial account, please have in mind the following considerations:

> * Choose host region `cf-us10` when creating a new trial account. This will ensure that all services required throughout the tutorial are available to your account.
> * If you use an existing trial account, make sure the host region is different from `cf-ap21`. Otherwise, some services required throughout the tutorial might be missing from your account. To check the host region for your account, choose **About** from the dropdown under your user in the top right corner of the SAP BTP Cockpit.

**Live:** There are multiple live landscapes available in different data centers around the globe. Live landscapes are intended for productive usage and development projects.


[DONE]
[ACCORDION-END]
---
[ACCORDION-BEGIN [Step 2: ](Create a Trial account)]
You can [register for a trial account](https://www.sap.com/cmp/td/sap-cloud-platform-trial.html) and access it in [SAP BTP Cockpit](https://cockpit.hanatrial.ondemand.com/cockpit#/home/trial).

A global account, a subaccount, a Cloud Foundry org, and space with some entitlements that are sufficient to do this tutorial are set up for you. You will only need to enable Kyma as described.

> In case you face a problem when creating a service instance or an application is missing for subscription later in the tutorial, please do the following:

> 1. Choose **Go To Your Trial Account**.
> 2. Choose **Account Explorer** and choose your **trial** subaccount in the **Subaccounts** tab.
> 2. Choose **Entitlements**.
> 3. Choose **Configure Entitlements**.
> 4. Choose **Add Service Plans**.
> 5. Search for the missing Service Plans and add it with **Add <x> Service Plans**.
> 6. Choose **Save**.

Continue with the following step [Configure `Kyma` in your subaccount](#configure-kyma-in-your-subaccount).

[DONE]
[ACCORDION-END]
---
[ACCORDION-BEGIN [Step 3: ](Create a Live account)]
If you choose to create an account on Live, you have to select a number of services that you need to subscribe to, for example, an SAP HANA database. For each service, there are so-called `entitlements`, which are basically the service plans and the number of units that you want from each service. When you create an account, you need to provide these also.

The following services with their service plans and entitlements are required for the different modules of the tutorial and will be needed to create the global account and subaccount.



| Service                           | Plan       | Amount | Unit         | Tutorial                                |
| --------------------------------- | ---------- | ------ | ------------ | --------------------------------------- |
| Kyma runtime             | `Kyma Runtime Trial`     | 1      | GB           | [Prepare for SAP BTP Development](btp-app-#configure-kyma-in-your-subaccount)   |
| SAP HANA Schemas & HDI Containers | `hdi-shared` | 1      | instances    | [Set Up SAP HANA Cloud for Kyma](btp-app-kyma-hana-cloud-setup)   |
| SAP HANA Cloud                    | `hana`       | 1      | instances    | [Set Up SAP HANA Cloud for Kyma](btp-app-kyma-hana-cloud-setup)     |
| SAP Launchpad service             | `standard`   | 1      | active users | [Add the SAP Launchpad Service](btp-app-kyma-launchpad-service) |


> The following services are utility services, no entitlement needed:

| Service                          | Plan        | Amount | Unit         | Tutorial                                |
| -------------------------------- | ----------- | ------ | ------------ | --------------------------------------- |
| SAP HTML5 Application Repository service  | `app-host`    | 100    | MB        | [Add the SAP Launchpad Service](btp-app-kyma-launchpad-service)   |
| SAP Authorization and Trust Management service | `application` | 1      | instances    | [Deploy Your Application to Kyma](btp-app-kyma-deploy-application)   |

[DONE]
[ACCORDION-END]
---
[ACCORDION-BEGIN [Step 4: ](Create a subaccount)]
1. In SAP BTP cockpit enter your **Global Account**. If you are using a trial account, choose **Go To Your Trial Account**.

2. Choose **Account Explorer** in the left navigation pane.

3. Choose **Create** **&rarr;** **Subaccount**.

    !![Create subaccount](create_subaccount.png)

4. To fill the **New Subaccount** dialog, enter a **Display Name**.

    > Use a short name for your project and add the prefix for the landscape, for example: `<project name>-cf-us10`. Don't select the checkbox **Neo**!

5. Enter a subdomain.

    > Only valid HTTP domain characters are allowed.

6. Choose **Create**.

7. Wait for the completion of the subaccount creation.

8. Choose the tile with your new subaccount.

[DONE]
[ACCORDION-END]
---
[ACCORDION-BEGIN [Step 5: ](Assign entitlements)]
In this section, you assign a portion of the entitlements that you've bought for your global account to the individual subaccounts. In this, you have only one subaccount. If you have 3 subaccounts, for example, and have bought 100 units of the HTML5 service, you could assign 50 units to the first subaccount, 20 to the second, and the remaining 30 to the third subaccount.

1. In your subaccount, choose **Entitlements** in the left-hand pane.

2. Choose **Configure Entitlements**.

3. Choose **Add Service Plans**.

4. Go through the Entitlements according to the table in the previous step **Create a Live Account** and add the required plans for each of them.

5. Choose the + or - symbol to change the quota for the services according to the table in the previous step **Create a Live Account**.

6. Choose **Save**.

[DONE]
[ACCORDION-END]
---
[ACCORDION-BEGIN [Step 6: ](Configure Kyma in your subaccount)]
This creates a Kyma instance in your subaccount that is a full-blown `kubernetes` cluster with Kyma on top.

1. In your subaccount's **Overview** page, choose the **Kyma Environment** tab and choose **Enable Kyma**.

    !![Enable Kyma](enable_kyma.png)

2. In the **Enable Kyma** dialog, a plan, an instance name, and a cluster name are automatically filled for you. You can keep the default settings and choose **Create**.


    !![Set plan, instance name, and cluster name](kyma_instance_name.png)

    > Prefer to use a different instance name?

    > We recommend you use a CLI-friendly name to enable the managing of your instances with the SAP BTP command line interface as well.

    > A CLI-friendly name is a short string (up to 32 characters) that contains only alphanumeric characters (A-Z, a-z, 0-9), periods, underscores, and hyphens. It can't contain white spaces.

    > As mentioned, when you create an environment instance that enables an environment you want to use, the name is generated automatically for you. You can use that name or replace it with the name of your choice.

3. The creation of the cluster takes some time. When done, you should see a **Console URL**, a **KubeconfigURL**, and the name of your cluster.

    !![Kyma Enabled](kyma_enabled.png)


[VALIDATE_1]
[ACCORDION-END]
---
