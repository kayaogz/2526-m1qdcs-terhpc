# 2526-m1qdcs-terhpc

Please make sure that your name appears in the list of registered students (if not please add it): https://cirrus.universite-paris-saclay.fr/s/E55T4HoNWnZZx23

In this TER project, we will develop, using AI-driven HPC software development, a fully functional and optimized BLAS library that rivals the performance of OpenBLAS; a hand-tuned optimized multithreaded BLAS/LAPACK implementation.

# Organization

* We will be using Google Antigravity IDE as the AI assistant tool (https://antigravity.google). With your university account, you can get a one-year free Google Gemini student membership (https://gemini.google/students/); please go ahead and activate your Gemini account, which we will use as the AI backend of the Antigravity IDE.

* I will give you access to a 20-core Intel CPU workstation. For this, I will need you to put your SSH key in the registration sheet. Please put your **public ssh key (ending with .pub)** on ssh key column in the spreadsheet above. There you will find the ssh command to connect to your account on the remote machine.

* At the beginning of each session, I would like to have each group a mini talk/presentation of 5-6 minutes, sharing their experience regarding their work in the previous week. This will be an informal exchange; you do not need a polished talk or slides. Talking points: what worked, what did not work, challenges faced, how managed to overcome, etc. This will also give you little bouts of storyline for your final presentation and report.

## Week 1: Getting warmed up with Antigravity and tiled matrix multiplication (13/03)

Goals for the week

* Installing and setting up antigravity

* Setting up connection to the remote workstation through Antigravity

* Launching agents and creating a OpenMP Hello World program that displays thread id and number of threads.

* 8x8 matrix multiplication micro-kernel development using AVX2+FMA

* Higher level code that performs L3, L2, and L1 tiling, and uses the 8x8 microkernel for multiplication.

* Testing and verification of the implementation (make sure it is correct)

* Benchmarking against single threaded OpenBLAS.

## Week 2: Tiled matrix multiplication (cont.) (27/03)

## Week 3: Tiled matrix multiplication (cont.) (03/04)

## Week 4: BLAS 1 kernels (only s???? type, excluding strided versions) (10/04)

## Week 5: BLAS 2 kernels (only s???? type, excluding strided versions) (17/04)

## Week 6: Other BLAS 3 kernels (trsm, syrk, trmm) (tentative) (24/04)

## Week 7: TER Presentations (to be announced later)


# Evaluation

Your course grade will be calculated as follows:

1. Project implementation
* You should send your completed lab assignment completed to my university mail (oguz.kaya[at]universite-paris-saclay.fr) with subject line "M1QDCSTERHPC PROJECT Firstname1 LASTNAME1 Firstname2 LASTNAME2" (e.g., M1QDCSTERHPC PROJECT Jean-François DURAND Julie DUFONT).
* In your e-mail, please attach all your project content in a single .zip file (and make sure it does not exceed 20MB).
* If you have a partner/binome for the lab assignment, please send me **one e-mail per group**.
* You should send your work no later than **30/04 Thursday 23:59:59**

2. Project report
* You will write a 20-30 page report on your implementation. There is no fixed format, but make sure to use 11pt policy, single column page format, margins no less than 2cms.
* The report should ideally contain following points:
* A short introduction outlining the project goals and background (no more than 3 pages).
* For each BLAS kernel (or group of kernels), I would like to see the approaches you tried (and succeeded/failed) using AI-driven development. What worked, what did not work, how much improvement did you get applying each optimization, when did AI failed so you had to intervene, when it succeded, etc.
* Experimental section that compares your code's performance to OpenBLAS library

3. Project presentation
* Project presentations will take place together with other individual TER projects, sometime in May. You will receive an e-mail from the TER coordinator (Pablo Arnault) regarding this.
* You will have 15 minutes to present + 5-10 minutes for questions. 
* In the presentation, you will not have time to present all your results. You should rather focus on your experience with AI-driven HPC development, what worked, what did not work, and lessons learned, together with some major results (of GEMM kernel for example).

# Tips and advices

* Since all of you will be sharing a single machine, it is important to make a fair use of the CPU resources. In particular, try to optimize the single threaded version of the code first. Once it is efficient, you can run the multi-core benchmarks. For multi-core benchmarks, limit the thread count to 8 for most runs. Once you have a production-ready code, you can benchmark up to 16 threads.

* When using Antigravity, try to use the Gemini Flash model as much as possible; it is remarkably good and you have much higher credit limit. You can save Gemini Pro credits for more critical optimization/organization/code generation tasks. Your credit limit resets about every 4 hours.

# References

* https://github.com/OpenMathLib/OpenBLAS

* https://antigravity.google
