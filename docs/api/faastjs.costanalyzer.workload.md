[Home](./index) &gt; [faastjs](./faastjs.md) &gt; [CostAnalyzer](./faastjs.costanalyzer.md) &gt; [Workload](./faastjs.costanalyzer.workload.md)

## CostAnalyzer.Workload interface

A user-defined cost analyzer workload for [CostAnalyzer.analyze()](./faastjs.costanalyzer.analyze.md)<!-- -->.

Example:

<b>Signature:</b>

```typescript
interface Workload<T extends object, A extends string> 
```

## Properties

|  Property | Type | Description |
|  --- | --- | --- |
|  [concurrency](./faastjs.costanalyzer.workload.concurrency.md) | `number` | The amount of concurrency to allow. Concurrency can arise from multiple repetitions of the same configuration, or concurrenct executions of different configurations. This concurrency limit throttles the total number of concurrent workload executions across both of these sources of concurrency. Default: 64. |
|  [format](./faastjs.costanalyzer.workload.format.md) | `(attr: A, value: number) => string` | Format an attribute value for console output. This is displayed by the cost analyzer when all of the repetitions for a configuration have completed. The default returns `${attribute}:${value.toFixed(1)}`<!-- -->. |
|  [formatCSV](./faastjs.costanalyzer.workload.formatcsv.md) | `(attr: A, value: number) => string` | Format an attribute value for CSV. The default returns `value.toFixed(1)`<!-- -->. |
|  [repetitions](./faastjs.costanalyzer.workload.repetitions.md) | `number` | The number of repetitions to run the workload for each cost analyzer configuration. Higher repetitions help reduce the jitter in the results. Repetitions execute in the same FaastModule instance. Default: 10. |
|  [silent](./faastjs.costanalyzer.workload.silent.md) | `boolean` | If true, do not output live results to the console. Can be useful for running the cost analyzer as part of automated tests. Default: false. |
|  [summarize](./faastjs.costanalyzer.workload.summarize.md) | `(summaries: WorkloadAttribute<A>[]) => WorkloadAttribute<A>` | Combine [CostAnalyzer.WorkloadAttribute](./faastjs.costanalyzer.workloadattribute.md) instances returned from multiple workload executions (caused by value of [CostAnalyzer.Workload.repetitions](./faastjs.costanalyzer.workload.repetitions.md)<!-- -->). The default is a function that takes the average of each attribute. |
|  [work](./faastjs.costanalyzer.workload.work.md) | `(faastModule: FaastModule<T>) => Promise<WorkloadAttribute<A> | void>` | A function that executes cloud functions on `faastModule.functions.*`<!-- -->. The work function should return `void` if there are no custom workload attributes. Otherwise, it should return a [CostAnalyzer.WorkloadAttribute](./faastjs.costanalyzer.workloadattribute.md) object which maps user-defined attribute names to numerical values for the workload. For example, this might measure bandwidth or some other metric not tracked by faast.js, but are relevant for evaluating the cost-performance tradeoff of the configurations analyzed by the cost analyzer. |
