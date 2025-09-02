# Know the possible Biases in the Data

Our social metrics, like all software metrics, are an approximation of
the real world. There will always going to be corner cases and biases in the
data. In particular, there are some situations where the metrics don’t
perform as well. So please read the following section in order to
minimize the bias in the analysis results.

## Developers with Multiple Aliases

A developer may end up with multiple aliases. Perhaps they’re committing
from both a personal- and a company account. Or they’ve changed their
e-mail address. This introduces a bias in the data since CodeScene uses the name of each developer as their identification.

Fortunately, this bias is easy to avoid by utilizing a Git feature
called `.mailmap`. A `.mailmap` is a file that you include in the root of
your Git repository. The file specifies a mapping from multiple names and
addresses to the canonical name and address of each developer with multiple
aliases. It’s straightforward to use a .mailmap, so please check out the [git
log documentation](https://git-scm.com/docs/git-shortlog) for the format.

## Autosquash Commits

Some teams may use a Git feature called *autosquash*. This feature is a
way of re-writing the development history. It may be fine if squashing
is used for the work of an individual developer. Unfortunately the
feature is sometimes used to combine the work of multiple programmers
into a single commit.

The consequence is that the analyses lose important data for temporal
coupling and, in particular, the social metrics become more limited than
they’d have to be. For example, it’s not possible to generate a
knowledge map over individual programmers, which means that you miss the
opportunity to use the analysis methods for on- and off-boarding.

It’s highly recommended that you reconsider the autosquash strategy in
case you apply it today. In general, the work of multiple programmers
should not be compressed in a single commit.

## Pair Programming

The knowledge metrics in CodeScene are based on the author of
the code as recorded by Git. This may obviously be misleading if your
organization does pair-programming.

A future version of CodeScene will address pair-programming
knowledge by having the option to fetch the author names from the commit
message instead and assign the knowledge to both authors. However, in
the current version there’s no such option.

If you use pair-programming you’re also likely to rotate pairs on a
daily basis. In that case, we recommend that you ignore the analysis of
individual developers and focus on your team knowledge map instead,
which will have accurate data.
