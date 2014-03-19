## Design

[edited 20140319; continues item 4 from https://github.com/sudowhoami/regex-engine/blob/master/High_level_design_thoughts.md]

### Idea: Diminishing index of plausible next steps

1. Traverse target once and make "candidate" list of indices bearing elements that match the first element of the search string.

        candidate = []

1. For each item in candidate list, compare `target[item+1]` against the second element of the search string. Prune candidate list accordingly.
1. Repeat until search string is exhausted (success) or candidate list is empty (failure).
1. Problem: each optional-content item still creates multiple lists that have to be handled. Should this be done as sublists within `candidate` or should separate `candidate` objects be instantiated and treated in parallel?

### Operators:

1. default: literal characters match literally
1. `.`: any character matches; no additional candidate list created? or multiple such lists
1. `|`: either of two characters or groups match; if both do, then one additional candidate list created
1. `?`: one character or group matches or does not match; one additional candidate list created
1. `*`: multiple additional candidate lists may be created
1. `+`: multiple additional candidate lists may be created
1. `[...]`: multiple additional candidate lists may be created
1. `(...)`: group can be treated as a subproblem of the same type

[end]