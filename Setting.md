# Android studio setting (mac 기준)

## style xml import

- 설정 -> Editor -> Code Style -> Schema 를 "Project" 로 설정 후 아래 값 변경
  - Preferences
    - Code style
      - General
        - → Hard wrap at 300 자로 설정(자동으로 코드가 내려가는 것을 방지하기 위해 최대한 멀리 위치 시킴)
      - Kotlin
        - Tabs and Indents
          - → Tab size : 4
          - → Indent : 4
          - → Countinuation intdent : 4
        - Blank lines
          - Keep maximum blank lines
            - → in declarations : 1
            - → in code: 1
        - Imports
          - → Insert imports for inner classes 체크 해제
      - Xml
        - Tab and Indents
          - → Tab size : 4
          - → Indent : 4
          - → Countinuation intdent : 4
         
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
