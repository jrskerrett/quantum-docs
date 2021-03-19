---
author: KittyYeungQ
description: This document provides a basic guide to submit and run Q# applications in Azure Quantum using Python.
ms.author: kitty
ms.date: 02/01/2021
ms.service: azure-quantum
ms.subservice: core
ms.topic: conceptual
title: Submit jobs to Azure Quantum with Python
uid: microsoft.quantum.submit-jobs.python
---

# Submit jobs to Azure Quantum with Python

This document provides a basic guide to submit and run Q# applications in Azure
Quantum using Python.

## Prerequisites

- An Azure Quantum workspace in your Azure subscription. To create
  a workspace, see [Create an Azure Quantum workspace](xref:microsoft.quantum.workspaces-portal).

## Installation

Follow these steps to install Jupyter Notebook and the current version of the
IQ# kernel, which powers the Q# Jupyter Notebook and Python experiences.

1. Install [Miniconda](https://docs.conda.io/en/latest/miniconda.html) or
   [Anaconda](https://www.anaconda.com/products/individual#Downloads).
1. Open an Anaconda Prompt.
   - Or, if you prefer to use PowerShell or pwsh: open a shell, run `conda init
     powershell`, then close and re-open the shell.
1. Create and activate a new conda environment named `qsharp-env` with the
   required packages (including Jupyter Notebook and IQ#) by running the
   following commands:

    ```
    conda create -n qsharp-env -c quantum-engineering qsharp notebook

    conda activate qsharp-env
    ```

1. Run `python -c "import qsharp"` from the same terminal to verify your
   installation and populate your local package cache with all of the required QDK
   components.

You are now set up to use Python and Q# integration to run
quantum programs on Azure Quantum.

## Quantum computing with Q# and Python

1. The Python environment in the conda environment that you created earlier already
   includes the `qsharp` Python package. Make sure you are running your Python
   script from a terminal where this conda environment is activated.

1. If you've never used Q# with Python, follow the steps in [Create your first Q#
   program with
   Python](xref:microsoft.quantum.install-qdk.overview.python).

1. Write your Q# operations in a `*.qs` file. When running `import qsharp` in
   Python, the IQ# kernel will automatically detect any .qs files in the same
   folder, compile them, and report any errors. If compilation is successful,
   those Q# operations will become available for use directly from within
   Python.
    - For example, the contents of your .qs file could look something like this:

        ```qsharp
        namespace Test {
            open Microsoft.Quantum.Intrinsic;
            open Microsoft.Quantum.Measurement;
            open Microsoft.Quantum.Canon;

            operation GenerateRandomBits(n : Int) : Result[] {
                use qubits = Qubit[n];
                ApplyToEach(H, qubits);
                return MultiM(qubits);
            }
        }
        ```

1. Create a Python script in the same folder as your `*.qs` file. Azure Quantum
   functionality is available by running `import qsharp.azure` and then calling
   the Python commands to interact with Azure Quantum. For reference, see the
   [complete list of `qsharp.azure` Python commands](https://docs.microsoft.com/python/qsharp-core/qsharp.azure).
   You'll need the resource ID of your Azure Quantum workspace in order to
   connect. (The resource ID can be found on your workspace
   page in the Azure Portal.)

   If your workspace was created in an Azure region other than \"West US\", you also
   need to specify this as the `location` parameter to `qsharp.azure.connect()`.

   For example, your Python script could look like this:

    ```py
    import qsharp
    import qsharp.azure
    from Test import GenerateRandomBits

    qsharp.azure.connect(
       resourceId="/subscriptions/.../Microsoft.Quantum/Workspaces/WORKSPACE_NAME",
       location="West US")
    qsharp.azure.target("ionq.simulator")
    result = qsharp.azure.execute(GenerateRandomBits, n=3, shots=1000, jobName="Generate three random bits")
    print(result)
    ```

    where `GenerateRandomBits` is the Q# operation in a namespace `Test` that is
    defined in your `*.qs` file, `n=3` is the parameter to be passed to
    that operation, `shots=1000` (optional) specifies the number of repetitions
    to perform, and `jobName="Generate three random bits"` (optional) is a custom
    job name to identify the job in the Azure Quantum workspace.

1. Run your Python script by running the command `python test.py`, where `test.py` is
   the name of your Python file. If successful, you should see your job results
   displayed to the terminal. For example:

   ```output
   {'[0,0,0]': 0.125, '[1,0,0]': 0.125, '[0,1,0]': 0.125, '[1,1,0]': 0.125, '[0,0,1]': 0.125, '[1,0,1]': 0.125, '[0,1,1]': 0.125, '[1,1,1]': 0.125}
   ```

1. To view the details of all jobs in your Azure Quantum workspace, run the command `qsharp.azure.jobs()`:

   ```dotnetcli
   >>> qsharp.azure.jobs()
   [{'id': 'f4781db6-c41b-4402-8d7c-5cfce7f3cde4', 'name': 'GenerateRandomNumber 3 qubits', 'status': 'Succeeded', 'provider': 'ionq', 'target': 'ionq.simulator', 'creation_time': '2020-07-17T21:45:43.4405253Z', 'begin_execution_time': '2020-07-17T21:45:54.09Z', 'end_execution_time': '2020-07-17T21:45:54.101Z'}, {'id': '1b03cc74-b5d5-4ffa-81db-465f08ae6cd0', 'name': 'GenerateRandomBit', 'status': 'Succeeded', 'provider': 'ionq', 'target': 'ionq.simulator', 'creation_time': '2020-07-21T19:44:17.1065156Z', 'begin_execution_time': '2020-07-21T19:44:25.85Z', 'end_execution_time': '2020-07-21T19:44:25.858Z'}]
   ```

1. To view the detailed status of a particular job, pass the job ID to `qsharp.azure.status()` or `qsharp.azure.output()`, for example:

   ```dotnetcli
   >>> qsharp.azure.status('1b03cc74-b5d5-4ffa-81db-465f08ae6cd0')
   {'id': '1b03cc74-b5d5-4ffa-81db-465f08ae6cd0', 'name': 'GenerateRandomBit', 'status': 'Succeeded', 'provider': 'ionq', 'target': 'ionq.simulator', 
   'creation_time': '2020-07-21T19:44:17.1065156Z', 'begin_execution_time': '2020-07-21T19:44:25.85Z', 'end_execution_time': '2020-07-21T19:44:25.858Z'}

   >>> qsharp.azure.output('1b03cc74-b5d5-4ffa-81db-465f08ae6cd0')
   {'0': 0.5, '1': 0.5}
   ```

## Next steps

Now that you know how to submit jobs to Azure Quantum, you can try to run the different [samples](https://github.com/microsoft/qio-samples) we have
available or try to submit your own projects.