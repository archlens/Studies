**1 - Logging**

_1a_
Implement a `Logger` class in the Infra folder with three methods that format and print the input to the console. `LogInformation`, `LogWarning` and `LogError`. The methods do not return anything, only prints the input.

Acceptance criteria:
- There is a `Logger` class in the Infra folder (remember to add correct namespace)
- There is a `LogInformation` method taking in a string, printing "INFO: {input}"
- There is a `LogWarning` method taking in a string, printing "WARN: {input}"
- There is a `LogError` method taking in a string, printing "ERROR: {input}"

_1b_
Use the logger to log the size of the result of running serialization in the `DependencyGraphSerializer`.

Acceptance criteria:
- When serialization finishes, before the result is returned, the size of the byte[] is logged at information level
- If the byte[] is empty, it is logged at warning level instead


_1c_
Use the logger instead of `Console.Error` in `DependencyGraphBuilder`.

Acceptance criteria:
- In `TryClassifyItem` the logger logs the exception at error level
- In `ParseFileItemAsync` the logger logs the exception at error level


_1d_
Use the logger to log at information level whether `UpdateGraphUseCase` is running with diff or not.

Acceptance criteria:
- `UpdateGraphUseCase` logs "Running diff use case" if diff is true
- `UpdateGraphUseCase` logs "Running non-diff use case" if diff is false


**2 - Exclusions**

_2a_
All the logic for exclusions that is currently in the  `ChangeDetector` class should be moved to it own class called `ExclusionManager`.

Acceptance criteria:
- There is a class called `ExclusionManager` (remember to add correct namespace)
- The class contains the `ExclusionRule` record
- The class contains public methods:
  - `IsExcluded`
  - `NormalizeExclusionEntry`
  - `CompileExclusions`
- The class contains private methods:
  - `MatchesSuffixPattern`
  - `ToDirPrefix`
  - `GetRelative`
- All methods are static


**3 - Repository**

_3a_
Implement a basic Repository class, it should be in Infra and contain the methods `ProjectDependencyGraph? GetSnapshot()` and `void SetSnapshot(ProjectDependencyGraph snapshot)`. For now, `GetSnapshot` should always return null.

Acceptance criteria:
- There is a Repository class
- There is a `GetSnapshot` method that returns null
- There is a `SetSnapshot` method that takes in a ProjectDependencyGraph and currently does nothing


_3b_
Use the previously implemented `GetSnapshot` in the `UpdateGraphUseCase`, such that it uses the repository snapshot if it is not null, otherwise calls the `SnapshotManager`

Acceptance criteria:
- In `UpdateGraphUseCase`, `GetSnapshot` is called
- If `GetSnapshot` returns null, call `SnapshotManager`
- For testing reasons, it should be possible to run the use case without a repository


**4 - RendererBase**

_4a_
The `RendererBase` should normalize the `FileExtension` before using it. Beware of correct dots. See `ConfigManager.NormalizeExtension(ext)`

Acceptance criteria:
- `RendererBase` normalizes the `FileExtension`


**5 - ConfigManager**

_5a_
Instead of passing all the configs around, the `ConfigManager` should contain query methods for getting the different options.

Acceptance criteria:
- There is a `GetBaseOptions` method
- There is a `GetParserOptions` method
- There is a `GetRenderOptions` method
- There is a `GetSnapshotOptions` method
- The getters throw an exception if `LoadAsync` has not been run yet (and fields therefore are null)
- `LoadAsync` still returns the options, but only for the unit tests to work

_5b_
In `Program`, the `ConfigManager` is initialized and loaded. Factories receive the options they need using query methods, while the use case should take the whole config manager as a parameter.

Acceptance criteria:
- `Program` loads the config
- All three factories receive their options from config manager query methods
- The `UpdateGraphUseCase` receives the config manager as a parameter, and queries for the options when needed

_5c_
The loading of the configs should no longer be in the `ConfigManager` itself, but in a new `LoadConfigUseCase` that initializes the `ConfigManager`.

Acceptance criteria:
- There is a `LoadConfigUseCase` with a `RunAsync` method
- The use case contains all the logic for loading the config from the file, including relevant DTO's
- `RunAsync` initializes and returns the `ConfigManager`
- The `ConfigManager` now takes the four options as parameters in the constructor
- `Program.cs` runs the use case
