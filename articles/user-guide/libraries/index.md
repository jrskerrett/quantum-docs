---
author: cgranade
description: Overview of the standard, chemistry, and numerics libraries included in the Quantum Development Kit (QDK).
ms.author: chgranad
ms.date: 02/01/2021
ms.service: azure-quantum
ms.subservice: qsharp-guide
ms.topic: conceptual
no-loc: ['Q#', '$$v']
title: Quantum Development Kit Libraries
uid: microsoft.quantum.libraries.overview
---

# Overview of Q# Libraries
The Quantum Development Kit (QDK) is provided with several libraries to make it easier to develop quantum applications in Q#.
In this section of the documentation, we describe these libraries and how to use them in your programs.

- [**Standard libraries**](xref:microsoft.quantum.libraries.overview.standard.intro):
  This section describes the prelude, which defines the interface between Q# programs and target machines, and the canon, a Q# library that provides general-purpose operations and functions for use in writing Q# programs.
- [**Quantum chemistry library**](xref:microsoft.quantum.libraries.overview-chemistry.concepts.overview):
  This section describes the quantum chemistry library, which provides a data model for loading representations of fermionic Hamiltonians and quantum simulation operations and functions which act on these representations.
- [**Quantum numerics library**](xref:microsoft.quantum.libraries-numerics.overview):
  This section describes the quantum numerics library, which provides implementations for a host of mathematical functions. It supports integer (signed & unsigned) and fixed-point representations.
- [**Quantum machine learning library**](xref:microsoft.quantum.libraries-machine-learning.overview):
  This section describes the quantum machine learning library, which provides an implementation of the sequential classifiers that take advantage of quantum computing to understand data.

Sources of the libraries as well as code samples can be obtained from GitHub.
See [Licensing](xref:microsoft.quantum.libraries.overview.licensing) for further information. Note that package references ("binaries") are available also for the libraries and offer another way of including the libraries in projects.
A convenient way of obtaining them is via [NuGet](https://nuget.org).