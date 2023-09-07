# Julia Package Comparisons
This Github repository contains the content of INSERT LINK, a website that compares Julia Packages. The comparisons should be as simple to read and understand as possible.
The content should be the result of the combined perspectives of package developers and users to ensure the most fair and objective comparisons of packages.

It is currently hosted by a private github user. If the project catches on, it would ideally be moved to the [JuliaLang github organization](https://github.com/JuliaLang) due to it's potential importance to the general julia ecosystem.

## The problem to be adressed by this project
The Julia Package ecosystem is organic. This means that situations like the ones below occur all the time:
* A new package is registered. It uses a technically superior algorithm to achieve a goal that an existing package solves, but is less tested.
* There are 5 or more different packages that do the same thing in different ways (e.g. automatic differentiation).
* A new package is registered. It makes grand promises, and the documentation looks great. However it appears to be a one-man project, and you are unsure if it is tested or will continue to be maintained and developed.
* Two packages look interesting. You feel like one looks superior, but the other one has more stars.
* One package looks okay, another looks good. The good one is a wrapper of an existing python/C++ package.

Such situations, and many many more, will always be part of an organic package system. However, it can be hard to navigate. 
Currently, users will have to do one or more of the following to choose between competing/overlapping packages:
* Compare the number of stars, and the activity, of the github repository.
* Read the package announcements on [Discourse](https://discourse.julialang.org/c/package-announcements). Compare the number of hearts on the post, and read the comments.
* Ask for a comparison of specific packages on e.g. Discourse (Examples: INSERT LINKS).
* Read the documentation of both packages.
* Try to solve a simple test-problem with both packages, and see which one feels best.

The solutions above take increasingly more effort. Doing all of them is the best way to figure out which package is right for you, but it takes too much effort for many, especially when in the middle of a project where you need a package only for a specific part. The result is likely that many users never discover all the packages that could solve their problem, and definitly do not make a systematic comparison to find the ideal one.

Some packgages try to alleviate this problem by having a "See also" or "Related packges" section in the bottom of their readme. This is a bandaid-fix, as a) work is duplicated if each package repository has this section, and b) there are few guidelines on this section, and it style, existence and scope varies wildly.

Comparisons of packages in any package repository or in a discourse discussion are always suceptable to going out of date, as the organic package ecosystem is ever-changing. A good solution will therefore have to be updatable, and independent of any single package. A github-hosted website solves this issue, as anyone can make PR's and issues as things go out of date.

This project aims to create a canonical and updated website that will
1) make it easier for users to discover packages for specific problems/domains, and
1) learn about the differences between packages that overlap, to enable them to chose the most appropriate one.

# Sections and domains
The website will be organized into sections. Each section should cover a specific domain, e.g. plotting. The name of the section should make it clear 
to users which domain is covered in the section.

The format that makes the most sense will likely vary from domain to domain. Therefore, no general guidelines regarding the 
format of the comparisons will be made. If however a format emerges that works well, it might be imposed as the default format.

### ToDo's
* It would be great to automatically put e.g. an updated number of github stars on the website
* Make list of packages into links to repositories
* Writing the content for each section

# Webpage content from here
The goal is to create a github-hosted website, for which I plan to use [Franklin.jl](https://github.com/tlienart/Franklin.jl). Until then, I will write some content below to bootstrap this project. That content will be moved to the website once it is running.

## Plotting
Plots.jl, Makie.gl, Gaston.jl, PyPlot.jl

## Automatic Differentiation
Enzyme.jl, Zygote.jl, ...

## Uncertanty propagation
MontecarloMeasurements.jl and Measurements-jl

## Nonlinear numerical solvers
NonlinearSolve.jl, NLSolve.jl, Roots.jl, ...

## Machine learning
This section is concerned with general machine learning packages. A seperate section (link to section) exists for 
packages that only concern themselves with the sub-domain of Neural Networks.  
MLJ.jl, SciKitLearn.jl KNet.jl, HorseML

## Neural Networks
Flux.jl, Lux.jl, GradValley.jl

## Notebooks
Notebooks are a type of [Integrated Development Enviroment (IDE)](https://en.wikipedia.org/wiki/Integrated_development_environment), and 
are particularly useful for sharing and showing computations.  
Pluto.jl, IJulia.jl, Neptune.jl

## Multithreading/Accelerating loops
LoopVectorization.jl, Polyester.jl

## Dataframes
A dataframe is a data structure used to hold tabular data.  
DataFrames.jl, InMemoryDatasets.jl, JuliaDB.jl

## Linear Solvers
LinearSolve.jl, Paradiso.jl, MLK.jl, BandedMatrices.jl...  
See https://discourse.julialang.org/t/solving-sparse-linear-systems-fast/83071/9 
for a relevant discussion

## Serialization / Saving files
Jld.jl, JLD2.jl, Parquet.jl, Parquet2.jl

## Redefinable structs
Redefining a struct in base julia requires restaring the julia process. This can incur significant recompilation time (though this is greatly reduced in Julia 1.9 and 1.10).
These packages allow users to define structs that are redefinable.  
ProtoStructs.jl and RedefStructsRedfineStructs.jl  

See also Revise.jl for a different approach to struct redefinition.

## Digital Signal Processing
DSP.jl, SignalsBase.jl, SampledSignals.jl, SignalAnalysis.jl  

See also FFTW.jl

## Machine Learning Datasets
OpenML.jl, MLDatasets.jl

## Probabalistic Programming and Bayesian Inference
Turing.jl, Gen.jl, SOSS.jl, KissABC.jl, RxInfer.jl


- [MCMCChains.jl](https://github.com/TuringLang/MCMCChains.jl)

### Sampler
#### Hamiltonian Monte Carlo (gradient based)

- [DynamicHMC.jl](https://github.com/tpapp/DynamicHMC.jl)
- [AdvancedHMC.jl](https://github.com/TuringLang/AdvancedHMC.jl)
- [BarkerMCMC.jl](https://github.com/scheidan/BarkerMCMC.jl)

#### Adaptive MCMC (without gradient)

- [AdaptiveMCMC.jl](https://github.com/mvihola/AdaptiveMCMC.jl)
- [RobustAdaptiveMetropolisSampler.jl](https://github.com/anthofflab/RobustAdaptiveMetropolisSampler.jl)
- [KissMCMC.jl](https://github.com/mauro3/KissMCMC.jl)

## Peak finding
By "peak" we refer to a numerical value larger than any immediate neighbour. A simple example is a 
vector such as `[1, 2, 3, 1]`, which has a peak at it's third index. Functions also have peaks, but in a 
continous context. Multidimensional arrays/functions also have peaks, which are significantly harder to find.  

Peaks.jl, FindPeaks.jl, Images.jl
