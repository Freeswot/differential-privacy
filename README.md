# Differential Privacy

This project contains a set of libraries of ε- and (ε, δ)-differentially private
algorithms, which can be used to produce aggregate statistics over numeric data
sets containing private or sensitive information. The functionality is currently
available in C++ and Java.

Currently, we provide algorithms to compute the following:

| Algorithm          | C++           | Java  |
| -------------      |:-------------:| -----:|
| Count              | Supported     | Supported |
| Sum                | Supported     | Supported |
| Mean               | Supported     | Planned   |
| Variance           | Supported     | Planned   |
| Standard deviation |Supported      | Planned   |
|Order statistics (incl. min, max, and median) |Supported   | Planned |

We also provide an implementation of the Laplace and Gaussian mechanism that
can be used to perform computations that aren't covered by our pre-built
algorithms. 

All of these algorithms are suitable for research, experimental or production
use cases.

This project also contains a
[stochastic tester](https://github.com/google/differential-privacy/tree/master/differential_privacy/testing),
used to help catch regressions that could make the differential privacy
property no longer hold.

## How to Build

In order to run the differential private library, you need to install Bazel,
if you don't have it already. [Follow the instructions for your platform on the
Bazel website](https://docs.bazel.build/versions/master/install.html)

You also need to install Git, if you don't have it already.
[Follow the instructions for your platform on the Git website.](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)

Once you've installed Bazel and Git, open a Terminal and clone the
differential privacy directory into a local folder:

```git clone https://github.com/google/differential-privacy.git```

Navigate into the ```differential-privacy``` folder you just created,
and build the differential privacy library and dependencies using Bazel:


<!-- TODO: Update build instructions to reflect the new repo
     structure -->
To build the C++ library, run:
```bazel build differential_privacy/...```

To build the Java library, run:
```
cd java
bazel build ...
```

You may need to install additional dependencies when building the PostgreSQL
extension, for example on Ubuntu you will need these packages:

```sudo apt-get install libreadline-dev bison flex```

## Caveats

Differential Privacy requires some bound on maximum number of contributions
each user can make to a single partition. The libraries don't perform such
bounding.

The libraries implementation assumes that each user contributes only a single
row to each partition. It neither verifies nor enforces this; it is still the
caller's responsibility to pre-process data to enforce this bound.

We chose not to implement this step at the library level because it's not the
logical place for it - it's much easier to sort contributions by user and
combine them together with a distributed processing framework before they're
passed to our algorithms. You can use the library to build systems that allow
multiple contributions per user - [our paper](https://arxiv.org/abs/1909.01917)
describes one such system. To do so, multiple user contributions should be
combined before they are passed to our algorithms.


## Support

We will continue to publish updates and improvements to the library. We will not
accept pull requests for the immediate future. We will respond to issues filed
in this project. If we intend to stop publishing improvements and responding to
issues we will publish notice here at least 3 months in advance.

## License

[Apache License 2.0](LICENSE)

## Support Disclaimer

This is not an officially supported Google product.
