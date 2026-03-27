# A/B Tester Agent

## Overview

The A/B Tester agent designs, executes, and analyzes experiments to optimize agent performance through data-driven decisions.

## Core Concept

Experimentation workflow:
1. **Hypothesis Formation** - Define what to test and why
2. **Experiment Design** - Create test variants
3. **Traffic Allocation** - Distribute users to variants
4. **Data Collection** - Gather performance metrics
5. **Statistical Analysis** - Determine winner
6. **Implementation** - Deploy winning variant

## Skills

### Primary Skills
1. **Hypothesis Generation** - Create testable hypotheses
2. **Sample Size Calculation** - Determine required traffic
3. **Variant Design** - Create test variations
4. **Statistical Analysis** - Calculate significance
5. **Result Interpretation** - Draw actionable conclusions

### Secondary Skills
- Multi-armed bandit testing
- Sequential testing
- Segmentation analysis
- Guardrail metrics
- Novelty effect detection

## Use Cases

1. **Prompt Optimization** - Test different prompt variations
2. **UI Optimization** - Improve user interfaces
3. **Feature Testing** - Validate new features
4. **Algorithm Comparison** - Compare different approaches
5. **Pricing Experiments** - Test pricing strategies

## Example Experiments

### Prompt A/B Test
```json
{
  "experiment": {
    "name": "Customer Support Prompt v2",
    "hypothesis": "Adding empathy will improve satisfaction scores",
    "variants": {
      "control": {
        "prompt": "You are a customer support agent. Help the user.",
        "traffic": 50
      },
      "treatment": {
        "prompt": "You are an empathetic customer support agent. Acknowledge feelings, then help.",
        "traffic": 50
      }
    },
    "metrics": {
      "primary": "satisfaction_score",
      "secondary": ["resolution_time", "escalation_rate"],
      "guardrails": ["response_length", "safety_violations"]
    },
    "sample_size": 1000,
    "significance_level": 0.05
  }
}
```

### Feature Rollout Test
```json
{
  "experiment": {
    "name": "New Export Feature",
    "type": "feature_flag",
    "variants": {
      "control": {"feature_enabled": false, "traffic": 20},
      "treatment": {"feature_enabled": true, "traffic": 80}
    },
    "metrics": {
      "primary": "export_completion_rate",
      "secondary": ["time_to_export", "error_rate"]
    },
    "stopping_rules": {
      "min_sample": 500,
      "max_duration": "14d",
      "early_stop_threshold": 0.01
    }
  }
}
```

## Configuration

```json
{
  "agent_type": "ab-tester",
  "default_significance": 0.05,
  "default_power": 0.8,
  "min_sample_size": 100,
  "max_duration_days": 30,
  "traffic_allocation": "dynamic",
  "early_stopping": true,
  "segment_analysis": true,
  "auto_winner_implementation": false
}
```

## Statistical Methods

### Frequentist
```python
def frequentist_analysis(control, treatment, alpha=0.05):
    from scipy import stats
    t_stat, p_value = stats.ttest_ind(control, treatment)
    return {
        "significant": p_value < alpha,
        "p_value": p_value,
        "effect_size": cohens_d(control, treatment)
    }
```

### Bayesian
```python
def bayesian_analysis(control, treatment):
    import pymc3 as pm
    with pm.Model():
        mu_c = pm.Normal("mu_c", mu=0, sd=10)
        mu_t = pm.Normal("mu_t", mu=0, sd=10)
        diff = pm.Deterministic("diff", mu_t - mu_c)
        # ... model specification
        trace = pm.sample(1000)
    return {
        "prob_better": (trace["diff"] > 0).mean(),
        "expected_lift": trace["diff"].mean()
    }
```

### Sequential Testing
```python
def sequential_test(control, treatment, boundaries):
    z_score = calculate_z(control, treatment)
    n = len(control) + len(treatment)
    if z_score > boundaries.upper(n):
        return "significant_positive"
    elif z_score < boundaries.lower(n):
        return "significant_negative"
    return "continue"
```

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Time to significance | 2-14 days |
| False positive rate | 5% (controlled) |
| Power | 80% |
| Revenue lift per test | 5-15% |

## Integration Points

- Analytics platforms
- Feature flag systems
- Deployment pipelines
- Monitoring tools

## Monetization Strategy

### Pricing Tiers
- **Basic**: $0.10/experiment (simple A/B)
- **Pro**: $0.50/experiment (multivariate, segmentation)
- **Enterprise**: $2.00/experiment (Bayesian, auto-implementation)

### Target Markets
1. Product teams
2. Growth teams
3. AI/ML teams
4. Marketing teams

## Technical Implementation

```python
class ABTester:
    def __init__(self, significance=0.05, power=0.8):
        self.significance = significance
        self.power = power
        self.experiments = {}

    def create_experiment(self, config):
        exp = Experiment(
            name=config['name'],
            variants=config['variants'],
            metrics=config['metrics'],
            sample_size=self.calculate_sample_size(config)
        )
        self.experiments[exp.id] = exp
        return exp

    def calculate_sample_size(self, config):
        from statsmodels.stats.power import tt_solve_power
        return tt_solve_power(
            effect_size=config.get('expected_effect', 0.1),
            alpha=self.significance,
            power=self.power
        )

    def assign_variant(self, user_id, experiment_id):
        exp = self.experiments[experiment_id]
        return exp.assign(user_id)

    def record_metric(self, user_id, experiment_id, metric_name, value):
        exp = self.experiments[experiment_id]
        exp.record(user_id, metric_name, value)

    def analyze(self, experiment_id):
        exp = self.experiments[experiment_id]
        results = {}
        for metric in exp.metrics:
            results[metric] = self.statistical_test(
                exp.get_variant_data('control', metric),
                exp.get_variant_data('treatment', metric)
            )
        return ExperimentResult(exp, results)

    def get_winner(self, experiment_id):
        analysis = self.analyze(experiment_id)
        if analysis.primary_metric.significant:
            return analysis.primary_metric.better_variant
        return None
```

## Experiment Dashboard

```json
{
  "experiment": "Prompt Optimization v2",
  "status": "running",
  "days_running": 7,
  "sample_size": {
    "control": 523,
    "treatment": 527
  },
  "metrics": {
    "satisfaction_score": {
      "control_mean": 4.2,
      "treatment_mean": 4.5,
      "lift": "+7.1%",
      "p_value": 0.023,
      "significant": true
    },
    "resolution_time": {
      "control_mean": 120,
      "treatment_mean": 115,
      "lift": "-4.2%",
      "p_value": 0.15,
      "significant": false
    }
  },
  "recommendation": "Implement treatment - significant improvement in satisfaction"
}
```

## Related Agents

- `variant-generator/` - Generate test variants
- `results-analyzer/` - Deep analysis of results
- `feedback-processor/` - Qualitative feedback
