---
author: KittyYeungQ
description: Explanation of how to create applications for the different targets of Azure-Quantum
ms.author: kitty
ms.date: 02/01/2021
ms.service: azure-quantum
ms.subservice: core
ms.topic: conceptual
title: Create and run Q# applications in Azure Quantum
uid: microsoft.quantum.create-applications
---

# Create and run Q# applications in Azure Quantum

This guide outlines the process to create a Q# application and run it on the different quantum computing targets available in Azure Quantum. To see what types of quantum computing targets Azure Quantum offers, you can check our article [Targets in Azure Quantum](xref:microsoft.quantum.concepts.targets).

## Create and run applications for Full profile targets

**Full** profile targets can run any Q# program, meaning you can
write programs without functionality restrictions. Azure Quantum does not provide
any target with this profile yet, but you can try any Q# program locally using the
[full state simulator](xref:microsoft.quantum.machines.overview.full-state-simulator) or the [resources estimator](xref:microsoft.quantum.machines.overview.resources-estimator) from the QDK. 

If you need help setting up your environment to run Q# programs locally, see [Getting started with the QDK](xref:microsoft.quantum.get-started-qdk).

You can also explore different [Q# code samples](https://docs.microsoft.com/samples/browse/?languages=qsharp) to run locally with the QDK.

## Create and run applications for No Control Flow profile targets

**No Control Flow** profile targets can run a wide variety of Q# applications, with
the constraint that they can't use results from qubit measurements to control
the program flow. More specifically, values of type `Result` do not support
equality comparison.

For example, this operation can NOT be run on a No Control Flow target:

```qsharp
    operation SetQubitState(desired : Result, q : Qubit) : Result {
        if (desired != M(q)) {
            X(q);
        }
    }
```

Trying to run this operation on a No Control Flow target will fail because it evaluates a comparison between two results (`desired != M(q)`)
to control the computation flow with an `if` statement.

> [!NOTE]
> Currently, there is an additional limitation for this type of profile target: *you can't apply operations on qubits that have been measured, even
> if you don't use the results to control the program flow.* This limitation is
> not inherent to this profile type but is circumstantial to the situation of the Limited
> Preview.

Presently, these No Control Flow targets are available for Azure Quantum:

- **Provider:** IonQ
  - IonQ simulator (`ionq.simulator`)
  - IonQ QPU: (`ionq.qpu`)

### Create applications for IonQ targets

Follow these steps in this section to create an application to run in IonQ targets.

#### Prerequisites

- Install the [QDK](xref:microsoft.quantum.install-qdk.overview.standalone).
- A Quantum Workspace with IonQ listed as a provider. To create a Workspace, see [Create an Azure Quantum workspace](xref:microsoft.quantum.workspaces-portal).

#### Steps 

1. [Create a Q# application using the Q# project template.](xref:microsoft.quantum.install-qdk.overview.standalone)
1. Open the `*.csproj` file in a text editor (for example, VS Code) and edit the file to:
    - Make sure the project points to the latest version of the QDK. You can verify the latest version in the official [QDK Release Notes](xref:microsoft.quantum.relnotes-qdk).
    - Add a line specifying the target:
      - IonQ QPU: `<ExecutionTarget>ionq.qpu</ExecutionTarget>`
      - IonQ simulator: `<ExecutionTarget>ionq.simulator</ExecutionTarget>`
  
   Your `*.csproj` file should look something like this:
  
    ```xml
    <Project Sdk="Microsoft.Quantum.Sdk/X.XX.XXXXXXXX">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp3.1</TargetFramework>
        <ExecutionTarget>ionq.qpu</ExecutionTarget>
      </PropertyGroup>
    
    </Project>
    ```

   where `X.XX.XXXXXXXX` is a place holder for the number of the latest version of the QDK.
1. Write your Q# program, keeping in mind that you cannot compare measurement results to control the program flow. 
1. Build and run your program locally using the QDK local
   targets. These will let you know if your Q# application can run in IonQ's targets by checking the fulfillment of the No Control Flow restrictions and calculating the
   needed resources.
   - You can run your Q# program locally using the QDK full state simulator by
     using the command `dotnet run`. Since you selected the `ExecutionTarget` in
     the `*.csproj` file, the console output will warn you if you created a file that is not compatible with the No Control Flow profile.
   - You can use the
     [`resources estimator`](xref:microsoft.quantum.machines.overview.resources-estimator)
     to estimate what resources your Q# program requires to run. You invoke the resources estimator with the command: `dotnet run --simulator
     ResourcesEstimator`.
1. Once your Q# program is ready, submit the job to Azure Quantum
   using your preferred environment by using the target ID `ionq.qpu` for the QPU and `ionq.simulator` for the simulator.

For more information on how to submit jobs to Azure Quantum, see:

- [Submit jobs to Azure Quantum using the Azure CLI](xref:microsoft.quantum.submit-jobs.azcli).
- [Submit jobs to Azure Quantum using Python](xref:microsoft.quantum.submit-jobs.python).
- [Submit jobs to Azure Quantum using Q# Jupyter Notebooks](xref:microsoft.quantum.submit-jobs.jupyter)

## Create and run applications for Basic Measurement Feedback targets

**Basic Measurement Feedback** profile targets can run a wide variety of Q#
applications, with the constraint that you can only compare values of type `Result` as part of conditions within `if` statements in operations. The
corresponding conditional blocks may not contain `return` or `set` statements. This profile type supposes an improvement over No Control Flow profiles, but still is subject to
some limitations.

Currently, Azure Quantum doesn't host any targets with this profile,
however, we are planning to make some available during the Limited Review.

## Next steps

- Now that you know how to create Q# applications, you can learn more details about [how to submit jobs to Azure Quantum](xref:microsoft.quantum.submit-jobs.azcli). 
- You can also  try the different [samples](https://github.com/microsoft/qio-samples) we have available or try to submit your own projects.
