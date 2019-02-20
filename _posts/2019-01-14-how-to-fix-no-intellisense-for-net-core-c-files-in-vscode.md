---
ID: 5324
post_title: 'How to fix: No IntelliSense for .NET Core C# files in VSCode'
author: Roel van Lisdonk
post_excerpt: ""
layout: post
permalink: >
  https://www.roelvanlisdonk.nl/2019/01/14/how-to-fix-no-intellisense-for-net-core-c-files-in-vscode/
published: true
post_date: 2019-01-14 07:57:42
---
<p>When using the C# 1.17.1 Visual Studio Code extension, I didn't get correct IntelliSense for C# files.
</p><p>There was a problem with Omnisharp. It outputted the error found below.
</p><p>I also had Visual Studio Community 2017 installed and the Visual Studio Build Tools.
</p><p>After uninstalling the Visual Studio Build Tools. Visual Studio Code asked me to install necessary build tools, after clicking "Yes" to install, the problem was fixed.
</p><p>
 </p><p><strong>Error
</strong></p><p><span style="color:red">Omnisharp error in VSCode: Could not load SDK Resolver. A manifest file exists, but the path to the SDK Resolver DLL file could not be found.
</span></p><p>
 </p><p>
 </p><p>Starting OmniSharp server at 1/14/2019, 7:44:48 AM
</p><p>    Target: c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test
</p><p>
 </p><p>OmniSharp server started.
</p><p>    Path: C:\Users\roelv\.vscode\extensions\ms-vscode.csharp-1.17.1\.omnisharp\1.32.8\OmniSharp.exe
</p><p>    PID: 17140
</p><p>
 </p><p>[info]: OmniSharp.Stdio.Host
</p><p>        Starting OmniSharp on Windows 6.2.9200.0 (x64)
</p><p>[info]: OmniSharp.Services.DotNetCliService
</p><p>        DotNetPath set to dotnet
</p><p>[info]: OmniSharp.MSBuild.Discovery.MSBuildLocator
</p><p>        Located 3 MSBuild instance(s)
</p><p>            1: Visual Studio Build Tools 2017 15.9.28307.280 - "C:\Program Files (x86)\Microsoft Visual Studio\2017\BuildTools\MSBuild\15.0\Bin"
</p><p>            2: Visual Studio Community 2017 15.9.28307.280 - "C:\Program Files (x86)\Microsoft Visual Studio\2017\Community\MSBuild\15.0\Bin"
</p><p>            3: StandAlone 15.0 - "C:\Users\roelv\.vscode\extensions\ms-vscode.csharp-1.17.1\.omnisharp\1.32.8\msbuild\15.0\Bin"
</p><p>[info]: OmniSharp.MSBuild.Discovery.MSBuildLocator
</p><p>        Registered MSBuild instance: Visual Studio Build Tools 2017 15.9.28307.280 - "C:\Program Files (x86)\Microsoft Visual Studio\2017\BuildTools\MSBuild\15.0\Bin"
</p><p>[info]: OmniSharp.Cake.CakeProjectSystem
</p><p>        Detecting Cake files in 'c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test'.
</p><p>[info]: OmniSharp.Cake.CakeProjectSystem
</p><p>        Could not find any Cake files
</p><p>[info]: OmniSharp.WorkspaceInitializer
</p><p>        Project system 'OmniSharp.DotNet.DotNetProjectSystem' is disabled in the configuration.
</p><p>[info]: OmniSharp.MSBuild.ProjectSystem
</p><p>        No solution files found in 'c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test'
</p><p>[info]: OmniSharp.MSBuild.ProjectManager
</p><p>        Queue project update for 'c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test\core.test.csproj'
</p><p>[info]: OmniSharp.Script.ScriptProjectSystem
</p><p>        Detecting CSX files in 'c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test'.
</p><p>[info]: OmniSharp.Script.ScriptProjectSystem
</p><p>        Could not find any CSX files
</p><p>[info]: OmniSharp.WorkspaceInitializer
</p><p>        Invoking Workspace Options Provider: OmniSharp.Roslyn.CSharp.Services.CSharpWorkspaceOptionsProvider
</p><p>[info]: OmniSharp.WorkspaceInitializer
</p><p>        Configuration finished.
</p><p>[info]: OmniSharp.Stdio.Host
</p><p>        Omnisharp server running using Stdio at location 'c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test' on host 10684.
</p><p>[info]: OmniSharp.MSBuild.ProjectManager
</p><p>        Loading project: c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test\core.test.csproj
</p><p>[warn]: OmniSharp.MSBuild.ProjectManager
</p><p>        Failed to load project file 'c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test\core.test.csproj'.
</p><p>c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test\core.test.csproj(1,1)
</p><p>Microsoft.Build.Exceptions.InvalidProjectFileException: Could not load SDK Resolver. A manifest file exists, but the path to the SDK Resolver DLL file could not be found. Manifest file path 'C:\Program Files (x86)\Microsoft Visual Studio\2017\BuildTools\MSBuild\15.0\Bin\SdkResolvers\Microsoft.Build.NuGetSdkResolver\Microsoft.Build.NuGetSdkResolver.xml'. SDK resolver path: C:\Program Files (x86)\Microsoft Visual Studio\2017\BuildTools\Common7\IDE\CommonExtensions\Microsoft\NuGet\Microsoft.Build.NuGetSdkResolver.dll  c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test\core.test.csproj
</p><p>   at Microsoft.Build.Shared.ProjectFileErrorUtilities.VerifyThrowInvalidProjectFile(Boolean condition, String errorSubCategoryResourceName, BuildEventFileInfo projectFile, Exception innerException, String resourceName, Object[] args)
</p><p>   at Microsoft.Build.BackEnd.SdkResolution.SdkResolverLoader.TryAddAssemblyFromManifest(String pathToManifest, String manifestFolder, List`1 assembliesList, ElementLocation location)
</p><p>   at Microsoft.Build.BackEnd.SdkResolution.SdkResolverLoader.FindPotentialSdkResolvers(String rootFolder, ElementLocation location)
</p><p>   at Microsoft.Build.BackEnd.SdkResolution.SdkResolverLoader.LoadResolvers(LoggingContext loggingContext, ElementLocation location)
</p><p>   at Microsoft.Build.BackEnd.SdkResolution.SdkResolverService.Initialize(LoggingContext loggingContext, ElementLocation location)
</p><p>   at Microsoft.Build.BackEnd.SdkResolution.SdkResolverService.ResolveSdk(Int32 submissionId, SdkReference sdk, LoggingContext loggingContext, ElementLocation sdkReferenceLocation, String solutionPath, String projectPath, Boolean interactive)
</p><p>   at Microsoft.Build.BackEnd.SdkResolution.CachingSdkResolverService.&lt;&gt;c__DisplayClass3_0.&lt;ResolveSdk&gt;b__0(String key)
</p><p>   at System.Collections.Concurrent.ConcurrentDictionary`2.GetOrAdd(TKey key, Func`2 valueFactory)
</p><p>   at Microsoft.Build.BackEnd.SdkResolution.CachingSdkResolverService.ResolveSdk(Int32 submissionId, SdkReference sdk, LoggingContext loggingContext, ElementLocation sdkReferenceLocation, String solutionPath, String projectPath, Boolean interactive)
</p><p>   at Microsoft.Build.Evaluation.Evaluator`4.ExpandAndLoadImportsFromUnescapedImportExpressionConditioned(String directoryOfImportingFile, ProjectImportElement importElement, List`1&amp; projects, SdkResult&amp; sdkResult, Boolean throwOnFileNotExistsError)
</p><p>   at Microsoft.Build.Evaluation.Evaluator`4.ExpandAndLoadImports(String directoryOfImportingFile, ProjectImportElement importElement, SdkResult&amp; sdkResult)
</p><p>   at Microsoft.Build.Evaluation.Evaluator`4.EvaluateImportElement(String directoryOfImportingFile, ProjectImportElement importElement)
</p><p>   at Microsoft.Build.Evaluation.Evaluator`4.PerformDepthFirstPass(ProjectRootElement currentProjectOrImport)
</p><p>   at Microsoft.Build.Evaluation.Evaluator`4.Evaluate(ILoggingService loggingService, BuildEventContext buildEventContext)
</p><p>   at Microsoft.Build.Evaluation.Project.Reevaluate(ILoggingService loggingServiceForEvaluation, ProjectLoadSettings loadSettings, EvaluationContext evaluationContext)
</p><p>   at Microsoft.Build.Evaluation.Project.ReevaluateIfNecessary(ILoggingService loggingServiceForEvaluation, ProjectLoadSettings loadSettings, EvaluationContext evaluationContext)
</p><p>   at Microsoft.Build.Evaluation.Project.Initialize(IDictionary`2 globalProperties, String toolsVersion, String subToolsetVersion, ProjectLoadSettings loadSettings, EvaluationContext evaluationContext)
</p><p>   at Microsoft.Build.Evaluation.Project..ctor(String projectFile, IDictionary`2 globalProperties, String toolsVersion, String subToolsetVersion, ProjectCollection projectCollection, ProjectLoadSettings loadSettings, EvaluationContext evaluationContext)
</p><p>   at Microsoft.Build.Evaluation.ProjectCollection.LoadProject(String fileName, IDictionary`2 globalProperties, String toolsVersion)
</p><p>   at OmniSharp.MSBuild.ProjectLoader.EvaluateProjectFileCore(String filePath)
</p><p>   at OmniSharp.MSBuild.ProjectLoader.BuildProject(String filePath)
</p><p>   at OmniSharp.MSBuild.ProjectFile.ProjectFileInfo.Load(String filePath, ProjectLoader loader)
</p><p>   at OmniSharp.MSBuild.ProjectManager.LoadOrReloadProject(String projectFilePath, Func`1 loader)
</p><p>
 </p><p>[fail]: OmniSharp.MSBuild.ProjectManager
</p><p>        Attemped to update project that is not loaded: c:\Dev\GitHub\roelvanlisdonk\dev\c#\core\test\core.test.csproj
</p><p>
 </p><p>
 </p>