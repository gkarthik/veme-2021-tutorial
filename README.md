# Tutorial for VEME 2021

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/gkarthik/veme-2021-tutorial/HEAD?filepath=notebook%2Fexplore_jumps.ipynb)

This tutorial is based on the BEAST community tutorial available [here](https://beast.community/markov_jumps_rewards).

This tutorial will cover,
* Create XML to log Markov jump history.
* Create XML to log Markov jump history using an empirical tree distribution.

### Useful XML snippets,


Complete history logger

```
		<log id="completeJumpHistory" logEvery="100" fileName="batRABV.jumpHistory.log">
			<completeHistoryLogger>
				<markovJumpsTreeLikelihood idref="host.treeLikelihood"/>				
			</completeHistoryLogger>
		</log>
```

Empirical tree distribution
```
	<empiricalTreeDistributionModel id="treeModel" fileName="batRABV.trees">
		<taxa idref="taxa"/>
	</empiricalTreeDistributionModel>
	<statistic id="treeModel.currentTree" name="Current Tree">
		<empiricalTreeDistributionModel idref="treeModel"/>
	</statistic>
```

Operator for `currentTree`

```
		<empiricalTreeDistributionOperator weight="1">
			<empiricalTreeDistributionModel idref="treeModel"/>
		</empiricalTreeDistributionOperator>
```

