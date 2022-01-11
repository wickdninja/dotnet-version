# msbump

![image](https://user-images.githubusercontent.com/6932589/135706650-25dffc3b-ea0e-48b2-999c-2f88d55c6f9b.png)

CLI utility to bump versions of dotnet projects.

## Usage

You can use `npx` to execute directly or install globally.

`npx msbump --p path/to/project.csproj [major|minor|patch|build]`

OR

`npm i -g msbump`

`msbump --p path/to/project.csproj [major|minor|patch|build]`

### Args

<strong>--[path|project|p]</strong> is <strong>required</strong>, `[major|minor|patch|build]` optional, `--tag` Adds git tag optional

### Examples:

```
npx msbump --p ./tests/test.csproj --tag
Bumped Version to 1.0.0.1

npx msbump --p ./tests/test.csproj build
Bumped Version to 1.0.0.2

npx msbump --p ./tests/test.csproj patch
Bumped Version to 1.0.1.2

npx msbump --p ./tests/test.csproj minor
Bumped Version to 1.1.1.2

npx msbump --p ./tests/test.csproj major
Bumped Version to 2.1.1.2
```

### Using Build Targets

```xml
<Target Name="BumpBuildVersionOnDebugBuild" BeforeTargets="Build" Condition=" '$(Configuration)' == 'Debug'">
    <Exec Command="npx msbump --p ./*.csproj build" ContinueOnError="true">
      <Output TaskParameter="ExitCode" PropertyName="ErrorCode" />
    </Exec>
  </Target>
  <Target Name="BumpPatchVersionOnReleaseBuild" BeforeTargets="Build" Condition=" '$(Configuration)' == 'Release'">
    <Exec Command="npx msbump --p ./*.csproj patch" ContinueOnError="true">
      <Output TaskParameter="ExitCode" PropertyName="ErrorCode" />
    </Exec>
  </Target>
```
