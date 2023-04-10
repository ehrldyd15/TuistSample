# TuistSample


## 1. Project Initializer

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



