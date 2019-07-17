# 🔥 Official code guidelines for android of Knowre

- Knowre 안드로이드 공식 코드 스타일 가이드입니다.
- 모든 개발자는 본 가이드를 베이스로 코드를 작성하시기를 권고드립니다.
- 다만, 가이드가 모든 상황들을 다룰 수 없고 이미 정의된 룰이라 할지라도 예외는 발생할 수 있기 때문에 기본 참조용으로 사용합니다.
- 룰로 정해져있지 않는 상황, 예외, 수정제안등은 PR 부탁드립니다.

# Guidelines

- Guide for [General](https://github.com/taenguree/android-code-style-guide/blob/master/General.md) rules
- Guide for [Kotlin](https://github.com/taenguree/android-code-style-guide/blob/master/Kotlin.md) rules
- Guide for [Xml](https://github.com/taenguree/android-code-style-guide/blob/master/Xml.md) rules

# Studio setting (Mac 기준)

## style xml setting

- [구글 스타일 가이드 레포지토리](https://github.com/google/styleguide)를 clone
- 최상위 폴더에 있는 intellij-java-google-style.xml 파일을 안드로이드 스튜디오에 import 
  - AndroidStudio -> Preference -> Editor -> Code style -> Scheme
- 위 파일 import 후 아래와 같이 약간의 변경을 진행한다.
  - Preferences
    - Code style
      - General
        - → Hard wrap at 160 자로 설정
      - Kotlin
        - Tabs and Indents
          - → Tab size : 4
          - → Indent : 4
          - → Countinuation intdent : 8
        - Spaces
          - → 'if' parentheses 체크 해제
          - → 'for' parentheses 체크 해제
          - → 'while' parentheses 체크 해제
          - → 'catch' parentheses 체크 해제
          - → 'when' parentheses 체크 해제
        - Imports
          - → Insert imports for inner classes 체크 해제

## file template setting

- 기본적으로 클래스, 리소스 파일을 생성 시 /** Created By ... */ 와 같이 자동 생성되는 문구들이 없도록 한다.
- kt 파일의 경우 intenral 을 default 로 생성한다.
  - Preference
    - Editor
      - File and code Templates
        - Kotlin File
          ```
          #if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME}

          #end
          ```
        - Kotlin Class
          ```
          #if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME}

          #end

          internal class ${NAME} {
          }
          ```
        - Kotlin enum
          ```
          #if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME}

          #end

          internal enum ${NAME} {
          }
          ```
        - Kotlin interface
          ```
          #if (${PACKAGE_NAME} && ${PACKAGE_NAME} != "")package ${PACKAGE_NAME}

          #end

          internal interface ${NAME} {
          }
          ```


License
=======

    Copyright 2019 Taeyeon Jeon

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
