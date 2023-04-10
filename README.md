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
9) additionalFiles: Tuist에서 프로젝트를 만들때 Xcode에 자동으로 연결해주지 않는 파일을 넣으면 프로젝트에 연결시켜준다. 예를 들어서 README.md같은 파일은 프로젝트를 만들때 Xcode에는 자동으로 보여지지않는데 여기에 추가해준다면 Xcode에서도 볼 수 있다.
10) resourceSynthesizers: Tuist는 프로젝트를 생성할때 Resources/ 안에 파일 확장자에 따라 enum을 제공해준다.

## 2. Workspace.swift

