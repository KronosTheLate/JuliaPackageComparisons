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
* [Plots.jl](https://docs.juliaplots.org/) is the most used. It's probably the most documented, used in the most tutorials, and is used in many videos. 
    * Pros: Its main draw is that it has a lot of plugins to other packages through its recipes system, which means that a lot of odd things like `plot(sol::ODESolution)` or showing the sparsity of a `BandedMatrix` just works. With all of these integrations, it's normally what I would recommend first to newcomers since they will generally get the most done with the least work. It has a backend system, so you can make it generate plots via GR (the default), Plotly (i.e. make webpages), pyplot, PGFPlots (Latex output), UnicodePlots (i.e. output plots as text). This ease of use and flexibility is what its main draw is.
     * Cons: Its downside has traditionally been its startup time, though it's nearly a second now so that's fine. Its main downside now is mostly that it's not as configurable as something like Makie, and it's not as optimized if you get up to millions of points. Its flexibility means it's not just for standard plots but also for animations, building small graphical user interfaces, and building small apps. 
* [Makie](https://docs.makie.org/stable/) is probably the second most popular. It's natively Julia so it's cool in that aspect, you can see code all the way down. 
    * It's very optimized for large plots, especially with GPU acceleration via the OpenGL backend (GLMakie). It has a lot of examples these days. 
     * Its downside is that it's a bit less "first user friendly", given that its flexibility means there's a lot more options you're forced to specify everywhere. It has a recipe system now but it's fairly new and not well-integrated with most of the ecosystem, so it's not as seamless as Plots, though by 2024 I would assume that would largely be fixed. It has the longest startup time, used to be in minutes but now it's like 5-10 seconds. 
* [AlgebraOfGraphics.jl](https://aog.makie.org/stable/) is a grammar of graphics front-end to Makie. This essentially means it has an API that looks and acts like R's ggplot2. Thus it has largely the same pros and cons as Makie, since it's just calling Makie under the hood, but with the pro of being more familiar to users coming from R.
* [Gadfly](http://gadflyjl.org/stable/) is a grammar of graphics based library.
    * Pros: It's very familiar to a ggplot2 user. Its default theme is pretty nice looking.
    * Cons: It's a bit high on startup time, closer to Makie than Plots. Also, it's pretty feature poor. In particular, it is missing 3D plots, animations, the ability to make interactive apps with buttons, etc. For these reasons more and more people are adopting AlgebraOfGraphics, but if you're just doing some standard statistics it's fine.
* [Vega](https://www.queryverse.org/Vega.jl/stable) and [VegaLite](https://www.queryverse.org/VegaLite.jl/stable/) are of the same camp as Gadfly in the focus towards "standard" statistics and data science, but using wrappers to Javascript libraries. 
     * Pro: Fast startups 
     * Cons Similar to Gadfly, little to no flexibility (making apps, animations, ...) and integration with Julia libraries beyond Queryverse.
* [PlotlyLight](https://github.com/JuliaComputing/PlotlyLight.jl) is a no-frills wrapper to Plotly. 
    * Pro: No startup time
    * Cons: Requires reading the Plotly docs to know how to use it and has little flexibility or integration into Julia libraries.
* GR is a front end to a C library GR. It's actually used as the default front-end from Plots.jl. Many more people use it from Plots.jl than directly due to the integrations and docs, but it is nice for some things on its own.
    * Pros: It's fast, scales fairly well, has a fast startup time, has a nice GUI for investigating results, integrates well with ITerm, very flexible.
    * Cons: It's docs are bit difficult, and it doesn't have any integrations with Julia libraries. 
* [PGFPlotsX.jl](https://kristofferc.github.io/PGFPlotsX.jl/stable/) is a front-end to generate plots for Latex.
   * Pros: Fast startup, output to Latex which makes it easy to then further modify in publication documents.
   * Cons: Its interface is wonky, even if you are familiar with the pgfplots Latex package. This makes quite hard to use and teach. Very few integrations with Julia libraries (Measurements and Colors only?). Lacking flexibility in terms of animations and making apps, though it's quite flexible in its ability to modify the plots and make weird things.
* [UnicodePlots.jl](https://github.com/JuliaPlots/UnicodePlots.jl) is very simple, fast startup, and plots to text. Its downside of course is that text is the only output it has.
* [Gaston.jl](https://mbaz.github.io/Gaston.jl/v0.10.0/) a front-end to gnuplot.
     * Fast startup.
     * Pretty basic, lacking flexibility and integrations with Julia packages. Requires gnuplot so limitations on where it can be installed.
* [GMT.jl](https://github.com/GenericMappingTools/GMT.jl) is "generic mapping tools". It has some plotting tools [highlighted here](https://www.generic-mapping-tools.org/GMTjl_doc/examples/plotting_functions/).
    * Pros: Has good examples in the docs. Nice extra tools for maps.
    * Cons: Missing some standard plot types, limited integrations with other Julia packages.
* [GNUPlot.jl](https://github.com/gcalderone/Gnuplot.jl) uses gnuplot under the hood.
    * Pros: Instant startup, has some interesting data science integrations for things like named datasets, very complete set of plots
    * Cons: Not the most complete documentation, requires Linux with gnuplot.

### tl;dr

Plots.jl is the most used for a reason. It's very flexible, integrates with the most Julia packages so you'll find it all throughout other docs, and it has many of the advantages of the other libraries through its backend system. Thus if you needed Latex output, use the pgfplots backend. If you needed a webpage, use the Plotly backend. Unicodeplots backend when you want text output. Or the GR default for the basics. With Julia v1.9 its startup time is much improved (and it's like sub second on v1.10 beta), which was its major complaint before. If you're going to use one plotting library and don't care too much about every little detail, then Plots.jl is a good one to go with. It's definitely not the best in any of the cases, animations are better in Makie, Latex is better in PGFPlotsX, etc., but it's capable everywhere.

Makie.jl is catching up and may be the default in the near future. It scales well and its getting all of the niceties of Plots.jl. I wouldn't learn it first if you're new to Julia (right now, though that will likely change by 2024). But if you need animations or want to add custom buttons to a window (make a quick GUI-like thing), Makie is unmatched. If it makes its standard plotting interface a bit simpler, gets a few more integrations, and thus matches Plots.jl in simplicity, it may hit a "best of most worlds" soon.

Otherwise it's a bit domain specific. If you were using Plots.jl and needed more flexibility for publication-quality plots, PGFPlotsX.jl can help. Or if you prefer grammar of graphics, AlgebraOfGraphics.jl is good. If you're a stats person you may find Gadfly or VegaLite familiar, though I wouldn't recommend them first because these don't satisfy general user needs (try making a plot of an FEM output and see what I mean).

All of these are pretty good. You have a lot of options. In the end, pick the one that suits your needs best.

## Automatic Differentiation
Enzyme.jl, Zygote.jl, ...

## Uncertanty propagation
MontecarloMeasurements.jl and Measurements-jl

## Nonlinear numerical solvers
NonlinearSolve.jl, NLSolve.jl, Roots.jl, [SIAMFANLEquations.jl](https://github.com/ctkelley/SIAMFANLEquations.jl)

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

The author of Pluto.jl gave a talk ([YouTube link](https://youtu.be/Rg3r3gG4nQo?feature=shared)) at JupyterCon 2023, which features information about Pluto.jl and comparisons to Jupyter (IJulia.jl).

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

## Triangulations/Tessellations
In modeling, it is often neccesary to discretize space. This is often referred to as "triangulation" or ["tessellation"](https://en.wikipedia.org/wiki/Tessellation). This section is dedicated to packages that provide such functionality.

### Short summary
DelaunayTriangulation.jl is the most supported package for Delaunay triangulations in two dimensions. Delaunator.jl might be faster for unconstrained triangulations if you do not need exact arithmetic, and if you do not need constrained tesselations. In higher dimensions, you need Delaunay.jl if $n > 3$, or TetGen.jl is great if $n=3$.

### List of packages with short descriptions
- [DelaunayTriangulation.jl](https://github.com/DanielVandH/DelaunayTriangulation.jl): A pure Julia library for constructing planar triangulations with support for both unconstrained and constrained triangulations (including domains with holes, disjoint domains, etc.), mesh refinement, Voronoi tessellations, clipped and centroidal Voronoi tessellations, and dynamic updates. Uses exact geometric predicates and supports custom types.
- [VoronoiDelaunay.jl](https://github.com/JuliaGeometry/VoronoiDelaunay.jl): A pure Julia library that constructs planar triangulations and tessellations, although no support for constrained triangulations / mesh refinement or clipped / centroid tessellations. Restricts points to $[1, 2] \times [1, 2]$.
- [VoronoiCells.jl](https://github.com/JuliaGeometry/VoronoiCells.jl): A pure Julia library that extends VoronoiDelaunay.jl. This package provides useful tools for constructing and working with Voronoi tessellations. Supports clipping Voronoi cells to a specified rectangle. Like VoronoiDelaunay.jl, restricts points to $[1, 2] \times [1, 2]$.
- [Delaunay.jl](https://github.com/eschnett/Delaunay.jl): Wraps Python's main Delaunay triangulation library, [`scipy.spatial.Delaunay`](https://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.Delaunay.html), for computing Delaunay triangulations in $\mathbb R^N$. I don't believe constrained triangulations or mesh refinement is available here.
- [MiniQhull.jl](https://github.com/gridap/MiniQhull.jl): Wraps [Qhull](http://www.qhull.org/) for computing unconstrained Delaunay triangulations in $\mathbb R^N$. No support is provided for mesh refinement.
- [DirectQhull.jl](https://github.com/JuhaHeiskala/DirectQhull.jl/): Similar to MiniQhull.jl, although also provides support for convex hulls and Voronoi tessellations from Qhull.
- [Delaunator.jl](https://github.com/JuliaGeometry/Delaunator.jl): A pure Julia library modelled after the [JavaScript Delaunator library](https://github.com/mapbox/delaunator). This package can construct unconstrained triangulations of planar point sets. No support is available for constrained triangulations or mesh refinement, although support exists for computing the dual Voronoi tessellation. Centroidal tessellations are not implemented, although the Voronoi cells can be clipped to a bounding box. 
- [TriangleMesh.jl](https://github.com/konsim83/TriangleMesh.jl), [Triangulate.jl](https://github.com/JuliaGeometry/Triangulate.jl), [Triangle.jl](https://github.com/cvdlab/Triangle.jl): Interfaces to [Shewchuk's Triangle library](https://www.cs.cmu.edu/~quake/triangle.html).
- [TetGen.jl](https://github.com/JuliaGeometry/TetGen.jl): This is for Delaunay tetrahedralisation, wrapping [TetGen](https://wias-berlin.de/software/index.jsp?id=TetGen).
- [GMT.jl](https://github.com/GenericMappingTools/GMT.jl): A wrapper of [GMT](https://github.com/GenericMappingTools/gmt), allowing for [unconstrained Delaunay triangulations in two dimensions](https://www.generic-mapping-tools.org/GMTjl_doc/documentation/modules/triangulate/index.html#triangulate), and for [spherical triangulation, i.e. triangulation of points lying on a sphere](https://www.generic-mapping-tools.org/GMTjl_doc/documentation/modules/sphtriangulate/index.html#sphtriangulate).

Note that many of these are likely not maintained anymore - the last commit dates are, going from more to less recent:

- DelaunayTriangulation.jl: Sep 13, 2023 
- VoronoiDelaunay.jl: Jun 28, 2023 (This commit was to add a note that the package is only in maintenance mode)
- Delaunator.jl: May 50, 2023
- VoronoiCells.jl: Apr 12, 2023
- DirectQhull.jl: Mar 10, 2023
- Triangulate.jl: Oct 10, 2022
- MiniQhull.jl: Sep 29, 2022
- Triangle.jl: Jul 22, 2022
- TetGen.jl: Jun 2, 2022
- Delaunay.jl: May 12, 2022
- TriangleMesh.jl: May 27, 2021
