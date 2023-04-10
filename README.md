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
    
1) name: Target의 이름
2) platform: iOS, macOS, tvOS, watchOS 같은 플랫폼
3) product: app, appClips, staticFramework, framework, unitTest 등
4) productName: The built product name. 만들어진 product의 이름
5) bundleId: 프로젝트 파일을 열었을때 보이는 Bundle Identifier
6) deploymentTarget: 배포타겟을 설정할 수 있다. iOS, macOS, tvOS, watchOS가 있고 버전을 입력받는다. iOS같은 경우 디바이스도 받으면서 ipad, iphone, mac 3종류가 있다.
7) infoPlist: 기본으로 제공되는 것을 쓸 수도 있고 key 값에 따라 value를 넣어주면 커스텀으로 추가적으로 값을 넣어줄 수 있다. 또는 미리 Info.plist를 넣어놓고 경로를 줄 수도 있다.
8) sources: 소스 코드의 경로를 입력해주면 됩니다. [ ] 안에 문자열로 경로를 입력한다.
9) resources: 앞서서 resourceSynthesizers에서 Tuist가 Resources/ 의 리소스들을 자동으로 코드화한다고 했는데, 그때 이 리소스들이 어디에 있는지에 대한 경로다. sources와 같이 [ ] 안에 문자열로 경로를 입력한다.
10) copyFiles: Target에 대한 Build Phase 파일 복사 작업
11) headers: Target에 대한 headers
12) entitlements: Target에 대한 entitlements의 경로를 입력해준다.
13) scripts: Target에 대한 Build Phase 스크립트 작업
14) dependencies: Target의 의존성에 대한 것이고, 라이브러리나 다른 모듈을 의존성으로 넣을 때 쓴다.
15) settings: Target의 세팅을 정의
16) coreDataModels: CoreData의 모델들의 경로랑 버전을 정의
17) environment: scheme에서 Edit Scheme... 버튼을 누르면 나오는 창에서 Environment Variables를 설정할 수 있는데 이때 environment를 설정하면 자동으로 생성한다.
18) launchArguments: scheme에서 Edit Scheme... 버튼을 누르시면 나오는 창에서 Arguments Passed On Launch를 설정할 수 있는데 이때 launchArguments 설정하면 자동으로 생성한다.
19) additionalFiles: 프로젝트를 생성할때 자동으로 생겨나지 않는 파일을 등록해놓으면 Xcode에서 볼 수 있다.


