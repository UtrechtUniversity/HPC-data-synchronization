# HPC-data-synchronization
This guide provides instructions for data synchronization (or data staging) in workflows involving High Performance Computing platforms such as the UBC cluster, Cartesius or Lisa. 

##Issue
When you take the step of performing data-analyses (or simulations) from a PC to High Performance Computing (HPC) platforms, you are faced with new challenges of managing data, by running analyses on multiple platforms (e.g. on both your PC and an HPC platform). Besides, file sizes may be too large to efficiently store it locally on your PC and HPC clusters are typically not meant for long-term storage of your data. Within this new infrastructure it is easy to lose track of the most recent versions of your datasets and scripts. Therefore, it is necessary to think of a workflow that allows efficient management of your data and scripts. 
Also for experienced users it is good to think about HPC workflows from time to time. Software tools and technology for data management and transfer are rapidly evolving and tools that were available a few years ago are replaced by new tools leading to new opportunities for saving time and keeping your workflow efficient and clear.

##Objective
This guide aims to provide instructions on how to manage and transfer your data efficiently when working on HPC platforms. It describes several solutions for different use cases and evaluates the performance of the different tools.
For questions and support contact Research IT via `info.rdm@uu.nl`


## Outline
A typical workflow for HPC calculations is outlined in the [Workflow](./Workflow.md) section. The different tools that are available are evaluated and discussed in the section [Evaluation of storage and transfer tools](./Evaluation.md). Instructions and automated scripts for data synchronization and transfer are available for the storage platforms that are explored in this test: I) [Yoda staging](./Yoda.md), II) [Surfdrive staging](./surfdrive.md), III) [Archive staging](./Archive.md)


Next: [Typical workflow](./workflow.md)

