# TuistSample


## Project.swift

    public init(
        name: String,
        organizationName: String? = nil,
        options: ProjectDescription.Project.Options = .options(),
        packages: [ProjectDescription.Package] = [],
        settings: ProjectDescription.Settings? = nil,
        targets: [ProjectDescription.Target] = [],
        schemes: [ProjectDescription.Scheme] = [],
        fileHeaderTemplate: ProjectDescription.FileHeaderTemplate? = nil,
        additionalFiles: [ProjectDescription.FileElement] = [],
        resourceSynthesizers: [ProjectDescription.ResourceSynthesizer] = .default
    )

1) name: 프로젝트의 이름 (name.xcodeproj)
2) organizationName: 프로젝트 파일의 inspector를 봤을때 있는 Organization에 들어가는 이름
3) Tuist가 xcodeproj 파일을 만들때의 옵션을 설정해줄 수 있다.
4) packages: Swift Package Manager의 package를 의미
5) settings: Build Settings의 정보들을 설정해준다. Dictionary로 값을 줄 수 있는데 값은 아래 링크
   (https://xcodebuildsettings.com/)
6) targets: 프로젝트의 타겟 (Target을 만들어서 Array로 넣어주면 그대로 만들어 준다.
7) schemes: 프로젝트의 scheme을 의미한다. Xcode로 프로젝트를 하나 열어서 중앙 최상단에서 약간 왼쪽을 보면 있는 Scheme들을 의미한다.
8) fileHeaderTemplate: 내장 Xcode 템플릿에 Custom으로 파일 헤더를 만들 수 있다.
9) additionalFiles: Tuist에서 프로젝트를 만들때 Xcode에 자동으로 연결해주지 않는 파일을 넣으면 프로젝트에 연결시켜준다. 예를 들어서 README.md같은 파일은 프로젝트를 만들때 Xcode에는 자동으로 보여지지않는데 여기에 추가해준다면 Xcode에서도 볼 수 있다.
10) resourceSynthesizers: Tuist는 프로젝트를 생성할때 Resources/ 안에 파일 확장자에 따라 enum을 제공해준다.

## Workspace.swift

    public init(
        name: String,
        projects: [ProjectDescription.Path],
        schemes: [ProjectDescription.Scheme] = [],
        fileHeaderTemplate: ProjectDescription.FileHeaderTemplate? = nil,
        additionalFiles: [ProjectDescription.FileElement] = [],
        generationOptions: ProjectDescription.Workspace.GenerationOptions = .options()
    )

1) name: 워크스페이스의 이름
2) projects: Workspace에 등록할 프로젝트들의 경로를 넣어주면 된다. struct인 Path를 받지만 그냥 문자열로 넣어주셔도 된다. 기본 경로는 프로젝트의 루트 디렉토리를 기준이다.
3) schemes, fileHeaderTemplate, additionalFiles: 위의 Project에서 설명과 동일
4) generationOptions: Tuist가 xcworkspace 파일을 만들때의 옵션을 설정해줄 수 있다.

## Config.swift

프로젝트 전역으로 쓰이는 설정을 설정해줄 수 있다. 

예를 들어서 Swift의 버전이나 Xcode의 버전 같은게 있다.
Config.swift는 {프로젝트 루트 디렉토리}/Tuist/Config.swift에 있을 때만 적용된다.

## Target

Project.swift에서 언급했던 Target이다. Target은 사용할 모듈을 정의하는 struct이다다.

    public init(
        name: String,
        platform: ProjectDescription.Platform,
        product: ProjectDescription.Product,
        productName: String? = nil,
        bundleId: String,
        deploymentTarget: ProjectDescription.DeploymentTarget? = nil,
        infoPlist: ProjectDescription.InfoPlist? = .default,
        sources: ProjectDescription.SourceFilesList? = nil,
        resources: ProjectDescription.ResourceFileElements? = nil,
        copyFiles: [ProjectDescription.CopyFilesAction]? = nil,
        headers: ProjectDescription.Headers? = nil,
        entitlements: ProjectDescription.Path? = nil,
        scripts: [ProjectDescription.TargetScript] = [],
        dependencies: [ProjectDescription.TargetDependency] = [],
        settings: ProjectDescription.Settings? = nil,
        coreDataModels: [ProjectDescription.CoreDataModel] = [],
        environment: [String : String] = [:],
        launchArguments: [ProjectDescription.LaunchArgument] = [],
        additionalFiles: [ProjectDescription.FileElement] = []
    )
    

