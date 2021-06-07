# Graph Differential Privacy

Implementations of differentially private release mechanisms for graph statistics.

Despite the extensive literature devoted to graph differential privacy, there is a paucity of open source tools that implement these techniques. As such, it is frequently the case that researchers that want to use or extend these results will need to build their own tools to do so.  In many cases, a differentially private release mechanism for graph statistics can be decomposed into two pieces: a computation step that produces exact query responses on an underlying graph and a perturbation step that adds noise to the exact query responses to achieve some level of differential privacy.

Computing the exact query responses involves working with the underlying graph data structure. There are many open source tools which provide efficient implementations of common graph algorithms. See for example
\cite{Bromberger17},
\cite{csardi2006}, \cite{hagberg2008exploring}, and \cite{peixoto_graph-tool_2014}. In some cases, these algorithms can be used directly to compute the statistics of interest. In other cases, these algorithms are used to produce lower-sensitivity approximations to a query of interest. For example, in \cite{kasiviswanathan2013analyzing} network flows on graphs derived from the original graph are used to compute query responses on arbitrary graphs with sensitivity similar to that of the query restricted to graphs with bounded degree.  

In this setting, the perturbation step amounts to a straight-forward application of the appropriate differentially private release mechanism. While many such release mechanisms are mathematically simple, creating secure implementations is fraught with peril.  As with cryptographic libraries, it is important to consider issues such as secure random number generation and robustness with respect to various side-channel attacks. Furthermore, because many differentially private release mechanisms operate on real numbers, as opposed to integers or floating point numbers that can be represented exactly in a computer, naive implementations of some mechanisms can be insecure. See for example \cite{mironov2012}. There are a number of open-source differential privacy libraries, see for example \cite{Gaboardi2020APF}, \cite{holohan2019diffprivlib}, \cite{rubinstein2017painfree}, and \cite{wilson2019differentially}. These libraries vary widely in the kinds of functionality that they provide, the security guarantees that they can offer, and the performance that they can achieve.  While most open-source libraries are sufficient for some tasks, e.g. research involving numerical simulations that is based on synthetic data, some may be insufficient for use in applications which will be used to protect real sensitive data.
 
To illustrate this approach, we have produced reference implementations of some of the algorithms described in \cite{kasiviswanathan2013analyzing}~\footnote{Available at: https://github.com/michaelpatrickpurcell/graph-dp} and \cite{nissim2007smooth}. 
These reference implementations use a new differential privacy library, RelM~\footnote{Code and documentation are available at https://github.com/anusii/RelM}, developed by one of the authors to perturb the data prior to release. RelM provides secure implementations of many of the differentially private release mechanisms described in \cite{dwork2014algorithmic}.

In cases where the computation of differentially private query responses cannot be decomposed into separate computation and perturbation steps, the situation is more grim.  We are unaware of any libraries that provide such functionality and as such any efforts to use or extend these algorithms will require the use of bespoke tools. 

