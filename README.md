# Tutorial for VEME 2021

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/gkarthik/veme-2021-tutorial/HEAD?filepath=notebook%2Fexplore_jumps.ipynb)

This tutorial is based on the BEAST community tutorial available [here](https://beast.community/markov_jumps_rewards).

This tutorial will cover,
* Create XML to log Markov jump history.
* Create XML to log Markov jump history using an empirical tree distribution.

For this tutorial you can downlaod the BEAST jar files from [here](https://github.com/beast-dev/beast-mcmc/releases/download/v1.10.5pre1/BEAST.v1.10.5pre.zip).

### Useful XML snippets,


Complete history logger

```
		<log id="completeJumpHistory" logEvery="100" fileName="batRABV.jumpHistory.log">
			<completeHistoryLogger>
				<markovJumpsTreeLikelihood idref="host.treeLikelihood"/>				
			</completeHistoryLogger>
		</log>
```

For complete history logger you need to add `useUniformization=”true” numberOfSimulants=”1” saveCompleteHistory=”true”` to the `markovJumpsTreeLikelihood` block.

```
	<!-- Likelihood for tree given discrete trait data                           -->
	<markovJumpsTreeLikelihood id="state.treeLikelihood" stateTagName="state.states" useUniformization="true" numberOfSimulants="1" saveCompleteHistory="true">
		<attributePatterns idref="state.pattern"/>
		<treeModel idref="treeModel"/>
		<siteModel idref="state.siteModel"/>
		<generalSubstitutionModel idref="state.model"/>
		<generalSubstitutionModel idref="state.model"/>
		<strictClockBranchRates idref="state.branchRates"/>

		<!-- START Ancestral state reconstruction                                    -->
		<!-- <parameter id="state.count" value=" 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 1.0 0.0"/> -->

		<!-- END Ancestral state reconstruction                                      -->

	</markovJumpsTreeLikelihood>
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

