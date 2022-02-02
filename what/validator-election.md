# Validator Election

The method by which validator nodes are selected to validate a block.
There are two main methods: top-weighted and rotating-selection.
Top-weighted just chooses the highest-rated nodes, and the validator-set basically
crystalizes over time (a node that can carry out many correct validations,
is likely to keep doing so). A rotating-selection involves choosing a subset of nodes
at random, and rotating them very frequently. This increases the degree of
decentralization, while top-weighted selection increases degree of centralization.