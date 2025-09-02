# Configure CodeScene for Pair Programming

If you use pair programming, CodeScene can adjust the knowledge maps by splitting the code contributions
between the members of each pair. CodeScene can deduce the contributing pair from either 1) the commit message, or
2) the author field. The options can be combined.

Configure your pair programming options in the Pair Programming part of your project configuration as
shown in [Fig. 200](#pair-programming-config).

![Configure patterns for pair programming](configuration/pair-programming-config.png)

CodeScene adjusts the knowledge maps by splitting the code contributions between the members of each pair.

The configuration is based on regular expressions with the following constraints:

1. It must contain at least one match group.
2. Each match group will map to exactly one author.

![Examples on pair programming](../shared/configuration/pair-programming-examples.png)

Similarly, CodeScene can also extract author information from the author field in Git. Use the second regular expression
for that.

Finally, if you wish to detect authors from both the author field **and** the commit message, enable the “Combine authors field and commit body to deduce pairs” option.
This requires setting a pattern for commit messages to detect the appropriate authors, if present.  The author field in Git will be used as-is unless you provide
a pattern.

## Configuration Examples

Most pair programming patterns contain some kind of delimiter in the commit message. The preceding examples used square brackets for
the pair programming info, [ and ], and a pipe | to separate the authors, but
CodeScene supports any delimiter like Pair: X,Y or (devs: X/Y).

The most common patterns are:

* *Always a pair*: Specify a pattern such that you get two match groups. For example, to match the authors in [Author X|Author Y] you use a pattern like `[([ws]+)|([ws]+)]`.
* *Sometimes a pair, sometimes an individual*: CodeScene defaults to Git’s Author information field if it cannot match the configured pattern, so this scenario will work with the previous pattern.
* *All author info is in the commit message*: In this case you need to make the second match group optional. For example, to match both the pair [Author X|Author Y] and the single developer [Author X] you specify `[([ws]+)|?([ws]+)?]`.
* *Many authors (a mob)*: To match more than two authors, we recommend that you introduce even more optional match groups. For example, to match [Author X|Author Y|Author Z] you specify `[([ws]+)|?([ws]+)?|?([ws]+)?]`.
* *Many authors (a mob or squashed commits)*: When a branch in GitHub is squashed and merged, the authors of the commits are aggregated into [Co-authored-by trailers](https://github.blog/2018-01-29-commit-together-with-co-authors/).
  To match the authors in Co-authored-by: Author Name <author@example.com> you specify a `Co-authored-by: ([ws.]+) <.*>` commit message pattern and enable the “Combine authors field and commit body to deduce pairs” option.
  Leave the author pattern blank, as CodeScene will automatically use the author in the Git Author field.

Those more elaborate patterns may be a bit tricky, but it’s a one off configuration so once you have it up and running you won’t see it again. Note
that the pattern will be recursively matched, and thus a single capture group can be used for finding multiple authors (like in the GitHub co-authors example).

For pair info that is specified in the author field, the following expression, `([ws]+)s+&s+([ws]+)`, would match an
author field specified as Author: Developer A & Developer B.

## Map Aliases for Authors in the Pairs

Finally, note that the preceding examples use aliases for each author instead of their full names. You can map those aliases to real author names using CodeScene’s UI
for developer identity aliases.
