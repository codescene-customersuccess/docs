# Social Networks

The *Social Network Analysis* gives you a heuristic on the coordination
needs between developers on different teams. The idea is based on
Conway’s law - a project works best when its organizational structure is
mirrored in software. Using the *Social Network Analysis*, you now have
a way to ensure that your organization matches the way the system is
designed with respect to the work the developers do.

## The Social Network Is Build from How the Code Evolves

The social network paths are mined from how your codebase is developed. You see an example
of a social network in code in [Fig. 152](#social-network-sample).

![An example of a social network in code](guides/social/SocialNetworkSample.png)

The network is built by identifying developers that repeatedly work in the
same parts of the code.
The more often they work in the same parts of the code, the stronger their link in the network. Note
that CodeScene filters developers with weak links since they would clutter the visualization.

## Define Your Development Teams

The social network lets you identify developers that should be close
from an organizational perspective. The visualization in [Fig. 152](#social-network-sample)
shows an example of an organization with 8 development teams. If you hover over a developer,
you highlight their peers that tend to work in the same parts of the codebase. You use this
information to evaluate how well your organization supports the way the codebase evolves.

That also means you want to compare your organizational chart with the information in
the generated social code network. Any discrepancies has to be understood.

## Align Your Architecture and Organization

In a perfect world most of your communication paths would be between
developers on the same team. That is, the teams have a meaning from an
architectural perspective; People on the same team work on the same
parts of the codebase. They share the same context, know each other and
have a much easier time coordinating their work.

However, sometimes the world looks radically different. Have a look at
[Fig. 153](#social-network-anti).

![An example of a social network anti-pattern](guides/social/SocialNetAntiPattern.png)

The visualization in [Fig. 153](#social-network-anti) shows an organization with severe coordination
problems. Since the data has been made anonymous to protect the guilty,
you cannot read the names of the teams or developers. But you still see
that the organization has four teams with a high degree of inter-team
coordination between virtually every developer. In practice, this isn’t
an organization with four different teams. Rather, it’s an organization
with one giant team of 29 developers with artificial organizational
boundaries between them. The resulting process loss due to coordination
needs is likely to be severe and lead to inefficient development,
quality issues and code that’s hard to evolve.
