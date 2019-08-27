# Android studio setting (mac 기준)

## style xml import

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
      - Xml
        - Tab and Indents
          - → Tab size : 4
          - → Indent : 4
          - → Countinuation intdent : 4
        - Other
          - Spaces → In empty tag 체크
         
## file template setting

- 기본적으로 클래스, 리소스 파일을 생성 시 /** Created By ... */ 와 같이 자동 생성되는 문구들이 없도록 한다.
- kt 파일의 경우 internal 을 default 로 생성한다.
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

## extra setting

- parameter name hint 를 disable 한다.
  - AndroidStudio -> Preference -> Editor -> General -> Appearance -> 'show parameter name hints' 체크해제
