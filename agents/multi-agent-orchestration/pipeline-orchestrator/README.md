# Pipeline Orchestrator Agent

## Overview

The Pipeline Orchestrator manages sequential task execution where output from one stage becomes input for the next. This pattern is ideal for well-defined processes with clear stages and dependencies.

## Core Concept

Pipeline flow:
1. **Stage Definition** - Define processing stages
2. **Data Flow** - Configure how data moves between stages
3. **Error Handling** - Define failure behaviors
4. **Monitoring** - Track progress through pipeline
5. **Output** - Collect final results

## Skills

### Primary Skills
1. **Stage Management** - Define and execute stages
2. **Data Transformation** - Convert outputs between stages
3. **Error Recovery** - Handle stage failures
4. **Progress Tracking** - Monitor pipeline progress
5. **Parallel Branching** - Execute parallel stages

### Secondary Skills
- Buffering and batching
- Rate limiting
- Caching intermediate results
- Checkpointing
- Replay from failure

## Use Cases

1. **Data Processing** - ETL workflows
2. **Content Pipeline** - Content creation workflows
3. **ML Pipelines** - Model training workflows
4. **CI/CD** - Deployment pipelines
5. **Document Processing** - Multi-stage document handling

## Example Pipelines

### Document Processing Pipeline
```json
{
  "pipeline": {
    "name": "Invoice Processing",
    "stages": [
      {
        "id": "extract",
        "agent": "pdf-extractor",
        "input": "raw_document",
        "output": "raw_text",
        "on_failure": "skip"
      },
      {
        "id": "parse",
        "agent": "structure-parser",
        "input": "raw_text",
        "output": "structured_data",
        "on_failure": "retry"
      },
      {
        "id": "validate",
        "agent": "validator",
        "input": "structured_data",
        "output": "validated_data",
        "on_failure": "manual_review"
      },
      {
        "id": "enrich",
        "agent": "data-enricher",
        "input": "validated_data",
        "output": "enriched_data",
        "on_failure": "continue"
      },
      {
        "id": "store",
        "agent": "database-writer",
        "input": "enriched_data",
        "output": "confirmation",
        "on_failure": "retry_3_times"
      }
    ]
  }
}
```

### ML Training Pipeline
```json
{
  "pipeline": {
    "name": "Model Training",
    "stages": [
      {"id": "data_fetch", "agent": "data-collector"},
      {"id": "preprocess", "agent": "data-preprocessor"},
      {"id": "feature_engineering", "agent": "feature-builder"},
      {
        "id": "train",
        "agent": "model-trainer",
        "parallel": {
          "models": ["random_forest", "xgboost", "neural_net"]
        }
      },
      {"id": "evaluate", "agent": "model-evaluator"},
      {"id": "deploy", "agent": "model-deployer", "condition": "accuracy > 0.9"}
    ],
    "checkpoints": ["preprocess", "train", "evaluate"]
  }
}
```

## Configuration

```json
{
  "agent_type": "pipeline-orchestrator",
  "execution_mode": "sequential",
  "max_parallel_stages": 5,
  "checkpoint_enabled": true,
  "checkpoint_frequency": "per_stage",
  "failure_strategy": "stop_on_error",
  "retry_count": 3,
  "timeout_per_stage": 300,
  "buffer_size": 1000,
  "output_format": "structured"
}
```

## Performance Characteristics

| Metric | Value |
|--------|-------|
| Throughput | High |
| Reliability | Very High |
| Debuggability | Excellent |
| Flexibility | Medium |
| Best for | Structured processes |

## Pipeline Patterns

### Linear Pipeline
Simple sequential stages:
```
A → B → C → D → E
```

### Parallel Branches
Multiple concurrent paths:
```
      ┌→ B1 →┐
A → B ├→ B2 →├→ C
      └→ B3 →┘
```

### Conditional Branches
Path based on conditions:
```
      ┌→ [if valid] → C1 →┐
A → B ├→ [if invalid] → C2 →├→ D
      └→ [if error] → C3 →─┘
```

### Fan-Out/Fan-In
Distribute and collect:
```
      ┌→ B1 →┐
      ├→ B2 →┤
A → B ├→ B3 →├→ C
      ├→ B4 →┤
      └→ B5 →┘
```

## Integration Points

- **n8n**: Visual pipeline builder
- **Apache Airflow**: Production pipelines
- **Prefect**: Modern workflow orchestration
- **Custom**: Any agent framework

## Monetization Strategy

### Pricing Tiers
- **Basic**: $0.10/pipeline (5 stages)
- **Pro**: $0.30/pipeline (unlimited stages, parallel)
- **Enterprise**: $1.00/pipeline (monitoring, SLAs)

### Target Markets
1. Data engineering teams
2. ML operations
3. Document processing services
4. CI/CD automation

## Technical Implementation

```python
class PipelineOrchestrator:
    def __init__(self, stages, config):
        self.stages = stages
        self.config = config
        self.state = {}
        self.checkpoints = {}

    def execute(self, initial_input):
        data = initial_input
        results = {'input': initial_input, 'stages': {}}

        for stage in self.stages:
            try:
                # Execute stage
                output = self.execute_stage(stage, data)

                # Store result
                results['stages'][stage['id']] = {
                    'input': data,
                    'output': output,
                    'status': 'success'
                }

                # Update data for next stage
                data = output

                # Checkpoint if enabled
                if self.config['checkpoint_enabled']:
                    self.save_checkpoint(stage['id'], data)

            except StageFailure as e:
                # Handle failure
                handling = stage.get('on_failure', 'stop')
                if handling == 'retry':
                    output = self.retry_stage(stage, data)
                elif handling == 'skip':
                    output = data  # Pass through
                elif handling == 'stop':
                    results['error'] = str(e)
                    return results

                results['stages'][stage['id']] = {
                    'status': 'recovered',
                    'handling': handling
                }

        results['output'] = data
        return results

    def execute_parallel(self, stages, data):
        with ThreadPoolExecutor(max_workers=self.config['max_parallel']) as executor:
            futures = {
                executor.submit(self.execute_stage, stage, data): stage
                for stage in stages
            }
            results = {}
            for future in as_completed(futures):
                stage = futures[future]
                results[stage['id']] = future.result()
            return results

    def recover_from_checkpoint(self, pipeline_id):
        last_checkpoint = self.get_last_checkpoint(pipeline_id)
        if last_checkpoint:
            return self.execute_from(last_checkpoint['stage'], last_checkpoint['data'])
        return None
```

## Pipeline Monitoring

```json
{
  "pipeline_run": {
    "id": "run_12345",
    "status": "in_progress",
    "current_stage": "enrich",
    "progress": 0.75,
    "stages": {
      "extract": {"status": "completed", "duration": "2.3s"},
      "parse": {"status": "completed", "duration": "1.1s"},
      "validate": {"status": "completed", "duration": "0.5s"},
      "enrich": {"status": "running", "started": "2026-03-28T10:00:00Z"},
      "store": {"status": "pending"}
    },
    "metrics": {
      "total_time": "4.2s",
      "estimated_remaining": "1.4s"
    }
  }
}
```

## Comparison with Other Patterns

| Aspect | Pipeline | Swarm | Hierarchy |
|--------|----------|-------|-----------|
| Flow | Sequential | Parallel | Hierarchical |
| Structure | Fixed | Emergent | Defined |
| Best for | Processes | Exploration | Management |
| Monitoring | Easy | Complex | Medium |

## Related Agents

- `plan-executor/` - Similar staged execution
- `swarm-coordinator/` - Parallel alternative
- `hierarchy-manager/` - Management alternative
