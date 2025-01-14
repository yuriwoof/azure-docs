---
title: Prepare to deploy Azure Communications Gateway 
description: Learn how to complete the prerequisite tasks required to deploy Azure Communications Gateway in Azure.
author: rcdun
ms.author: rdunstan
ms.service: communications-gateway
ms.topic: how-to
ms.date: 10/09/2023
---

# Prepare to deploy Azure Communications Gateway

This article guides you through each of the tasks you need to complete before you can start to deploy Azure Communications Gateway. In order to be successfully deployed, the Azure Communications Gateway has dependencies on the state of your Operator Connect or Teams Phone Mobile environments.

The following sections describe the information you need to collect and the decisions you need to make prior to deploying Azure Communications Gateway.

## Prerequisites

[!INCLUDE [communications-gateway-tsp-restriction](includes/communications-gateway-tsp-restriction.md)]

[!INCLUDE [communications-gateway-deployment-prerequisites](includes/communications-gateway-deployment-prerequisites.md)]

## Arrange onboarding

You need an onboarding partner to deploy Azure Communications Gateway. If you're not eligible for onboarding to Microsoft Teams through Azure Communications Gateway's [Included Benefits](onboarding.md) or you haven't arranged alternative onboarding with Microsoft through a separate arrangement, you need to arrange an onboarding partner yourself.

## Ensure you have a suitable support plan

We strongly recommend that you have a support plan that includes technical support, such as [Microsoft Unified Support](https://www.microsoft.com/en-us/unifiedsupport/overview) or [Premier Support](https://www.microsoft.com/en-us/unifiedsupport/premier).

## Choose the Azure tenant to use

We recommend that you use an existing Microsoft Entra tenant for Azure Communications Gateway, because using an existing tenant uses your existing identities for fully integrated authentication. If you need to manage identities separately from the rest of your organization, create a new dedicated tenant first.

The Operator Connect and Teams Phone Mobile environments inherit identities and configuration permissions from your Microsoft Entra tenant through a Microsoft application called Project Synergy. You must add this application to your Microsoft Entra tenant as part of [Connect Azure Communications Gateway to Operator Connect or Teams Phone Mobile](connect-operator-connect.md) (if your tenant does not already contain this application).

## Get access to Azure Communications Gateway for your Azure subscription

Access to Azure Communications Gateway is restricted. When you've completed the previous steps in this article, contact your onboarding team and ask them to enable your subscription. If you don't already have an onboarding team, contact azcog-enablement@microsoft.com with your Azure subscription ID and contact details.

Wait for confirmation that Azure Communications Gateway is enabled before moving on to the next step.

## Create a network design

Connectivity between your networks and Azure Communications Gateway must meet any relevant network connectivity specifications.

[!INCLUDE [communications-gateway-maps-or-expressroute](includes/communications-gateway-maps-or-expressroute.md)]

If you want to use ExpressRoute Microsoft Peering, consult with your onboarding team and ensure that it's available in your region.

Ensure your network is set up as shown in the following diagram and has been configured in accordance with any network connectivity specifications that you've been issued for your chosen communications services. You must have two Azure Regions with cross-connect functionality. For more information on the reliability design for Azure Communications Gateway, see [Reliability in Azure Communications Gateway](reliability-communications-gateway.md).

:::image type="content" source="media/azure-communications-gateway-redundancy.png" alt-text="Network diagram of an Azure Communications Gateway that uses MAPS as its peering service between Azure and an operators network.":::

You must decide whether you want Azure Communications Gateway to have an autogenerated `*.commsgw.azure.com` domain name or a subdomain of a domain you already own, using [domain delegation with Azure DNS](../dns/dns-domain-delegation.md). Domain delegation provides topology hiding and might increase customer trust, but requires giving us full control over the subdomain that you delegate. For Microsoft Teams Direct Routing, choose domain delegation if you don't want customers to see an `*.commsgw.azure.com` in their Microsoft 365 admin centers.

For Teams Phone Mobile, you must decide how your network should determine whether a call involves a Teams Phone Mobile subscriber and therefore route the call to Microsoft Phone System. You can:

- Use Azure Communications Gateway's integrated Mobile Control Point (MCP).
- Connect to an on-premises version of Mobile Control Point (MCP) from Metaswitch.
- Use other routing capabilities in your core network.

For more information on these options, see [Call control integration for Teams Phone Mobile](interoperability-operator-connect.md#call-control-integration-for-teams-phone-mobile) and [Mobile Control Point in Azure Communications Gateway](mobile-control-point.md).

If you plan to route emergency calls through Azure Communications Gateway for Operator Connect or Teams Phone Mobile, read [Emergency calling for Operator Connect and Teams Phone Mobile with Azure Communications Gateway](emergency-calling-operator-connect.md) to learn about your options.

## Configure MAPS or ExpressRoute

Connect your network to Azure:

- To configure MAPS, follow the instructions in [Azure Internet peering for Communications Services walkthrough](../internet-peering/walkthrough-communications-services-partner.md).
- To configure ExpressRoute Microsoft Peering, follow the instructions in [Tutorial: Configure peering for ExpressRoute circuit](../../articles/expressroute/expressroute-howto-routing-portal-resource-manager.md).

## Next step

> [!div class="nextstepaction"]
> [Deploy an Azure Communications Gateway resource and connect it to your networks](deploy.md)
