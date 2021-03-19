---
author: geduardo
description: List of common terms of the Azure Quantum service.
ms.author: v-edsanc
ms.date: 02/01/2021
ms.service: azure-quantum
ms.subservice: core
ms.topic: conceptual
title: Glossary for Azure Quantum
uid: microsoft.quantum.azure.glossary
---

# Glossary for Azure Quantum

**Azure Active Directory (AAD) / Microsoft Identity Platform** - Azure’s identity service, used to implement access control and authentication to resources. The names Azure Active Directory and Microsoft Identity Platform are interchangeable For more information, see [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-whatis).

**Azure Managed Application (AMA) / Managed Application** – A type of application offered to end customers in Azure through the Azure Marketplace. For more information, see [Azure managed applications](https://docs.microsoft.com/azure/managed-applications/overview).

**Azure Marketplace** – A storefront for cloud-based software in Azure. For more information, see [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/).

**Azure Quantum Job (Job)** – A program, problem, or application, submitted to Azure Quantum for processing by an Azure Quantum provider.

**Azure Quantum Job Target (Target)** – Providers expose one or more targets that can be used to run jobs. Customers select which target they would like to use to run a particular job. For example, a three-qubit machine and a six-qubit machine may each be targets.

**Azure Quantum Provider (provider)** – A provider is a component in Azure Quantum that provides the ability to run jobs. Providers may be made available by Microsoft or by third-party partners.

**Azure Quantum** – Microsoft’s quantum service for Azure, enabling customers access to quantum solutions from both Microsoft providers and partner providers.

**Azure Resource Manager (ARM)** – Azure’s deployment and management service. For more information, see [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).

**Quantum Development Kit (QDK)** - Microsoft’s software development kit for developing quantum applications in the Azure Quantum service. The QDK contains Q\#, Microsoft's programming language for quantum computing, along with Q\# libraries, samples and tutorials. It also contains developer APIs for running jobs on the Azure Quantum service. For more information, see the [Microsoft QDK Documentation](xref:microsoft.quantum.overview.qdk-overview)

**Quantum-Inspired Optimization Problem (QIO Problem)** - A problem expressed using our Python optimization library to be solved using Azure Quantum. Problems may be expressed as PUBOs (Polynomial Unconstrained Binary Optimization) or Ising forms.

**Quantum Program** - In the scope of Azure Quantum, a program written in Q# that targets a provider in Azure Quantum.

## Next steps

For more information, see:

- The [Microsoft Azure glossary](https://docs.microsoft.com/azure/azure-glossary-cloud-terminology)
- The [Quantum Development Kit glossary](xref:microsoft.quantum.glossary-qdk)