# PixInsight MCP execution and recovery

Use the PixInsight MCP connection available in the current environment. Before acting, inspect its current tool descriptions and schemas and identify the intended PI instance. Tool availability differs across MCP implementations and versions; never assume a named operation exists because another connector provides it.

## Capability discovery

Look for tools that support the required stage, such as:

- selecting or listing PI instances and open images;
- opening images, querying process parameters, and running processes;
- collecting image statistics, background measurements, noise estimates, or star metrics;
- executing verified PJSR when the connector supports it;
- saving images and reviewing history or checkpoints.

If a needed operation is not exposed, determine whether a documented and verified PJSR route is supported by the connected MCP. Adapt to the actual API; do not invent tool names or assume that a script can perform an operation merely because PI has a related process.

One observed `pardovot/pixinsight-mcp` tool route used `get_process_parameters` followed by `run_process`, `snapshot`/`restore`, `save_image`, and `run_script`. Treat these only as discovery examples: verify that the current connector exposes the operation and inspect its schema before use.

## Evidence for each run

1. Confirm the input image, source file, dimensions, channels, processing stage, and existing transformations.
2. Inspect current process parameters and accepted value formats. Set important values explicitly rather than relying on remembered UI state.
3. Check the returned result and errors. A text log or accepted parameter set alone does not prove that processing succeeded.
4. Confirm whether the intended image changed or a new view was created. For model-based background operations, verify both the model and the corrected target.
5. Compare before/after measurements and inspect consistent previews. Measurements supplement visual review; they do not replace it.

Process-specific interfaces can differ between scripts, GUI forms, and MCP schemas. Start with a small capability or parameter query and adapt based on evidence; avoid repeatedly submitting a complete workflow after an interface error. In connectors where `run_script` is available, its result may contain only the final expression value; console text alone is not proof of a structured result. DBE script data and GUI sample-table fields can also have different shapes or coordinate units. Query the current interface and test a minimal input before running a full correction, then inspect both the model and target image.

## Task ownership and resources

A single PI instance can be occupied by a long operation, and measurements may use the same execution channel. Do not compete with another task or close its windows. Keep one processing task at a time per instance, retain the baseline and selected result, and check memory and disk headroom before large images, masks, snapshots, or candidate batches.

Keep source files read-only and write outputs into a task-specific location. Before cleanup, verify the exact output location and preserve source data, useful calibration masters, verified checkpoints, selected layers, and files required by later stages. If ownership or recoverability is unclear, retain the file.

## Long tasks and recovery

Record the inputs, outputs, parameters, stage, and next action for long operations. A timeout does not prove that the operation stopped; inspect process state and outputs before retrying. If a targeted correction still produces the same error, stop that step, preserve the checkpoint, and report the limitation rather than repeating blindly.

Use a GUI only when the connected tools cannot complete a necessary step and an authorized UI-control route is available. Report only what the available tools actually confirmed.
