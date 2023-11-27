For sampling a function of $N$ variables, the range of each variable is divided into $M$ equiprobable intervals. 
Must know how many samples one wishes to take upfront and to keep track of those samples already taken.

Orthogonal sampling is better.

```python
def latin_hypercube_sampling(param_ranges, n_samples):
    rng = np.random.default_rng()
    perms = np.stack([rng.permutation(n_samples) for _ in param_ranges])
    hypercube = np.transpose(perms)
    deltas = [(r[1]-r[0])/n_samples for r in param_ranges]

    for sample in range(n_samples):
        params_ind = hypercube[sample]
        sampled_params = []
        
        for i, _ in enumerate(param_ranges):
            sampled_params.append(params_ind[i]*deltas[i])

        yield sampled_params
```
###### Tags
#MonteCarloMethods #SamplingMethods #ProbabilityTheory #NumericalMethods #StatisticalAnalysis