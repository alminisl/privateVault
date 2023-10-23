[[05-09-2022]] 

Writing the pipeline to the version on the sidebar. Currently my YML looks like this: 

```yml
name: $(BuildID)

resources:

    - repo: self

      clean: true

      fetchDepth: 1


pool:

    name: Vienna Win 

    demands: npm

  

variables:

    CI: true

  

steps:

    - task: NodeTool@0

      displayName: Install node

      inputs:

          versionSpec: "14.18.x"

          checkLatest: true

  

    - bash: |

          NPM_VERSION=$(yarn versions)

          VERSION_REGEX='.@vertigis/search-designer.: .([0-9]{1,2}.[0-9]{1,2}.[0-9]{1,2}).,'

          MERGE_REGEX='refs.pull.([0-9]+).merge'

          TAG_REGEX='refs.tags.(.+)'

          MASTER_REGEX='refs.heads.master'

          RELEASE_REGEX='refs.heads.release/.+'

  

          if [[ $NPM_VERSION =~ $VERSION_REGEX ]]; then

            VERSION=${BASH_REMATCH[1]}

  

            if [[ $BUILD_SOURCEBRANCH =~ $MASTER_REGEX ]]; then

              VERSION="$VERSION-dev.$BUILD_BUILDID"

            elif  [[ $BUILD_SOURCEBRANCH =~ $RELEASE_REGEX ]]; then

              VERSION="$VERSION-rc.$BUILD_BUILDID"

            elif  [[ $BUILD_SOURCEBRANCH =~ $TAG_REGEX ]]; then

              VERSION="${BASH_REMATCH[1]}"

            elif  [[ $BUILD_SOURCEBRANCH =~ $MERGE_REGEX ]]; then

              VERSION="$VERSION-pr${BASH_REMATCH[1]}.$BUILD_BUILDID"

            fi

          fi

          echo Version: $VERSION Branch: $BUILD_SOURCEBRANCH

          echo "##vso[task.setvariable variable=version]$VERSION"

      displayName: Create Version Number

      name: CreateVersionNumber

  

    - script: echo "##vso[build.updatebuildnumber]$VERSION"

      displayName: "Update Build Number"

  

    - script: yarn version --no-git-tag-version --new-version $(version)

      displayName: "Set Version Number"

  

    - script: yarn install

      displayName: "Install Dependencies"

  

    - script: yarn test

      displayName: "Running Tests"

      condition: succeeded()

  

    - script: yarn build

      displayName: "Build"

  

    - task: PublishBuildArtifacts@1

      displayName: "Publish Artifact: build"

      inputs:

          PathtoPublish: build

          ArtifactName: build```

This is a prototype pipeline, some expanation: 

// <mark style="background: #FF5582A6;">TODO </mark>
