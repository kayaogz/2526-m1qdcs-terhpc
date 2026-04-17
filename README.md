# 2526-m1qdcs-terhpc

In this TER project, we will develop, using AI-driven HPC software development, a fully functional and optimized BLAS library that rivals the performance of OpenBLAS; a hand-tuned optimized multithreaded BLAS/LAPACK implementation.

# Organization

* First of all, please make sure that your name and e-mail appears in the list of registered students (if not please add it): https://cirrus.universite-paris-saclay.fr/s/E55T4HoNWnZZx23

* We will be using Google Antigravity IDE as the AI assistant tool (https://antigravity.google). With your university account, you can get a one-year free Google Gemini student membership (https://gemini.google/students/); please go ahead and activate your Gemini account, which we will use as the AI backend of the Antigravity IDE.

* I will give you access to a 20-core Intel CPU workstation. For this, I will need you to put your SSH key in the registration sheet. Please put your **public ssh key (ending with .pub)** on ssh key column in the spreadsheet above. There you will find the ssh command to connect to your account on the remote machine.

* At the beginning of each week's session, I would like to have each group a mini talk/presentation of 5-6 minutes, sharing their experience regarding their work in the previous week. This will be an informal exchange; you do not need a polished talk or slides. Talking points: what worked, what did not work, challenges faced, how managed to overcome, etc. This will also give you little bouts of storyline for your final presentation and report.

* After the presentations, I will talk with each group and discuss the week's work, inspect the code, prompts, results, and give guidance for further development.

## Week 1: Getting started with Antigravity and tiled matrix multiplication SGEMM (13/03)

Goals for the week

* Installing and setting up antigravity

* Setting up connection to the remote workstation through Antigravity

* Launching agents and creating a OpenMP Hello World program that displays thread id and number of threads.

* 8x8 matrix multiplication micro-kernel development using AVX2+FMA

* Higher level code that performs L3, L2, and L1 tiling, and uses the 8x8 microkernel for multiplication.

* Testing and verification of the implementation (make sure it is correct)

* Benchmarking against single threaded OpenBLAS.

## Week 2: Tiled matrix multiplication (cont.) (27/03)

Goals for the week

* Make your GEMM implementation compatible with the Goto-BLAS algorithm, which uses L3 cache to hold a tile of B, L2 cache to hold a tile of A, and uses L1 cache as a workspace to fetch smaller tiles of A and B to multiply.

* Generate three different micro-kernels (lets say 8x8, 16x6, 4x24), and make the algorithm work with these. Generate assembly versions for each kernel as well. Benchmark the performance in each case.

* Add a 2D task-based parallelization; computing each tile (i,j) of C becomes a task. Also add a 3D variant with a constant k where k tasks will cooperate for computing a single tile (i,j) of C (with appropriate dependencies and tile sum/reduction in the end). Compare the multithreaded performance of each case.

* Generate generic multivariate performance auto-tuner for your kernels. The script must call the kernel as a function f(x1, x2, x3, ...) where each variable corresponds to a tunable parameter of your kernel (cache tiles sizes or microkernel type for matrix multiplication, loop unrolling factor for example). It should then navigate this parameter search space to find a quasi-optimal parameter set which yields the best performance. Such task is called **black-box optimization** for which many algorithms exist. The script should be able to use Stochastic Bayesian Optimization andtwo other algorithms of your choice. Compare the performance of all three algorithms (in best performance obtained / number of kernel calls).

## Week 3: Tiled matrix multiplication (cont.) (03/04)

* One of the important optimization techniques is **prefetching**; as the kernel is performing arithmetic operations on one tile, we can hint the processor to start loading the next tile into the cache. For this, the cache should be able to hold both existing and prefetched tiles simultaneously. Add this to your kernels and test the performance.

* So far, you have been generating and optimizing your kernels interactively with AI. Once you get the optimized implementation, it is preferable to have a complete implementation plan which allows us to generate this kernel from scratch with no a-priori conversation history with the AI. In other words, if you start a new project from scratch and give this implementation plan, AI should be able to generate a code that is as performant as your original implementation (or as close as possible).

## Week 4: BLAS 1 kernels (only s???? type, excluding strided versions) (10/04)

* Generate optimized AVX2 kernels for: sscal, scopy, sswap, saxpy, sdot, snrm2, sasum, isamax, srot.

* Add task-based parallelism as before.

* Aim to have a good implementation plan for one of the kernels, which should give a good baseline for other kernels since they all have similarities.

* You can assume incX and incY are both 1 for simplicity. If you desire you can also cover the cases with incX or incY >1.

* Make sure the signature of all your function exactly follows Fortran BLAS signature (sscal_(...)) and not CBLAS signature (cblas_sscal(...)) as you will later put all these into a library that will replace OpenBLAS in benchmark tests.

* Create a tester that automatically generates many test cases for each kernel (including edge/patological cases) and tests them thoroughly, by comparing against OpenBLAS.

## Week 5: BLAS 2 kernels (only s???? type, excluding strided versions) (17/04)

* Generate optimized AVX2 kernels for: sgemv, ssymv, strmv, strsv, sger, ssyr, ssyr2

* Add task-based parallelism as before.

* You can assume incX and incY are both 1 for simplicity. If you desire you can also cover the cases with incX or incY >1.

* Make sure the signature of all your function exactly follows Fortran BLAS signature (sgemv_(...)) and not CBLAS signature (cblas_sgemv(...)) as you will later put all these into a library that will replace OpenBLAS in benchmark tests.

## Week 6: Other BLAS 3 kernels (trsm, syrk, trmm) (tentative) (24/04)

* If you are motivated, you can also optionally try to generate optimized kernels for strsm, ssyrk, and/or strmm.

## Week 7: TER Presentations (date to be announced later)


# Evaluation

Your course grade will be calculated as follows:

1. Project implementation
* You should send your completed lab assignment completed to my university mail (oguz.kaya[at]universite-paris-saclay.fr) with subject line "M1QDCSTERHPC PROJECT Firstname1 LASTNAME1 Firstname2 LASTNAME2" (e.g., M1QDCSTERHPC PROJECT Jean-François DURAND Julie DUFONT).
* In your e-mail, please attach all your project content in a single .zip file (and make sure it does not exceed 20MB).
* Keep all your files as-is in the home folder of your account in the remote machine; I will be accessing and using it as well.
* If you have a partner/binome for the lab assignment, please send me **one e-mail per group**.
* You should send your work no later than **08/05 Friday 23:59:59**

2. Project report
* You will write a 20-30 page report on your implementation. There is no fixed format, but make sure to use 11pt policy, single column page format, margins no less than 2cms.
* The report should ideally contain following points:
* A short introduction outlining the project goals and background (no more than 3 pages).
* For each BLAS kernel (or group of kernels), I would like to see the approaches you tried (and succeeded/failed) using AI-driven development. What worked, what did not work, how much improvement did you get applying each optimization, when did AI failed so you had to intervene, when it succeded, etc.
* Experimental section that compares your code's performance to OpenBLAS library
* You should send your completed lab assignment completed to my university mail (oguz.kaya[at]universite-paris-saclay.fr) with subject line "M1QDCSTERHPC REPORT Firstname1 LASTNAME1 Firstname2 LASTNAME2" (e.g., M1QDCSTERHPC REPORT Jean-François DURAND Julie DUFONT).
* You should send your work no later than **08/05 Friday 23:59:59**

3. Project presentation
* Project presentations will take place together with other individual TER projects, sometime in May. You will receive an e-mail from the TER coordinator (Pablo Arnault) regarding this.
* You will have 15 minutes to present + 5-10 minutes for questions.
* In the presentation, you will not have time to present all your results. You should rather focus on your experience with AI-driven HPC development, what worked, what did not work, and lessons learned, together with some major results (of GEMM kernel for example).

# Tips and advices

* Since all of you will be sharing a single machine, it is important to make a fair use of the CPU resources. In particular, try to optimize the single threaded version of the code first. Once it is efficient, you can run the multi-core benchmarks. For multi-core benchmarks, limit the thread count to 8 for most runs. Once you have a production-ready code, you can benchmark up to 16 threads.
* When using Antigravity, try to use the Gemini Flash model as much as possible; it is remarkably good and you have much higher credit limit. You can save Gemini Pro credits for more critical optimization/organization/code generation tasks. Your credit limit resets about every 4 hours.
* Divide a task into many subtasks as much as possible; this will facilitate the work for the AI and make it use less compute time / credit.
# References

* https://github.com/OpenMathLib/OpenBLAS

* https://antigravity.google
