---
title: Configure Azure role-based access control (Azure RBAC) for Azure API for FHIR
description: This article describes how to configure Azure RBAC for the Azure API for FHIR data plane
author: matjazl
ms.service: healthcare-apis
ms.subservice: fhir
ms.topic: reference 
ms.date: 03/15/2020
ms.author: matjazl
ms.reviewer: dseven
---
# Configure Azure RBAC for FHIR 

In this article, you will learn how to use [Azure role-based access control (Azure RBAC)](../../role-based-access-control/index.yml) to assign access to the Azure API for FHIR data plane. Azure RBAC is the preferred methods for assigning data plane access when data plane users are managed in the Azure Active Directory tenant associated with your Azure subscription. If you are using an external Azure Active Directory tenant, refer to the [local RBAC assignment reference](configure-local-rbac.md).

## Confirm Azure RBAC mode

To use Azure RBAC, your Azure API for FHIR must be configured to use your Azure subscription tenant for data plane and there should be no assigned identity object IDs. You can verify your settings by inspecting the **Authentication** blade of your Azure API for FHIR:

:::image type="content" source="media/rbac/confirm-azure-rbac-mode.png" alt-text="Confirm Azure RBAC mode":::

The **Authority** should be set to the Azure Active directory tenant associated with your subscription and there should be no GUIDs in the box labeled **Allowed object IDs**. You will also notice that the box is disabled and a label indicates that Azure RBAC should be used to assign data plane roles.

## Assign roles

To grant users, service principals or groups access to the FHIR data plane, click **Access control (IAM)**, then click **Role assignments** and click **+ Add**:

:::image type="content" source="media/rbac/add-azure-rbac-role-assignment.png" alt-text="Add Azure role assignment":::

In the **Role** selection, search for one of the built-in roles for the FHIR data plane:

:::image type="content" source="media/rbac/built-in-fhir-data-roles.png" alt-text="Built-in FHIR data roles":::

You can choose between:

* FHIR Data Reader: Can read (and search) FHIR data.
* FHIR Data Writer: Can read, write, and soft delete FHIR data.
* FHIR Data Exporter: Can read and export (`$export` operator) data.
* FHIR Data Contributor: Can perform all data plane operations.

In the **Select** box, search for a user, service principal, or group that you wish to assign the role to.

>[!Note]
>Make sure that the client application registration is completed. See details on [application registration](register-confidential-azure-ad-client-app.md)
>If OAuth 2.0 authorization code grant type is used, grant the same FHIR application role to the user. If OAuth 2.0 client credentials grant type is used, this step is not required.

## Caching behavior

The Azure API for FHIR will cache decisions for up to 5 minutes. If you grant a user access to the FHIR server by adding them to the list of allowed object IDs, or you remove them from the list, you should expect it to take up to five minutes for changes in permissions to propagate.

## Next steps

In this article, you learned how to assign Azure roles for the FHIR data plane. To learn about additional settings for the Azure API for FHIR:
 
>[!div class="nextstepaction"]
>[Additional settings for Azure API for FHIR](azure-api-for-fhir-additional-settings.md)
