# How to Integrate SonarQube with React/Javascript Projects

## Getting Started

##### 1) Download and setup SonarQube

- Download SonarQube from [HERE](https://www.sonarqube.org/downloads/)
    - Start SonarQube from /bin/{OS}/StartSonar.bat
    - Login using http://localhost:9000
    - Username and Password is _admin_ by default
    - Create a new project and generate a _token_
    

- Download Sonar-Scanner zip file for Javascript [HERE](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/)
    - Add to _/bin_ path variable and verify
    - Add below properties to _/conf/sonar-scanner.properties_ file
        - sonar.host.url=http://localhost:9000
        - sonar.sourceEncoding=UTF-8
        

##### 2) Add properties inside project folder
    
- Create a new file _sonar-project.properties_ inside project folder
- Add below properties to the file
    ```
        # must be unique in a given SonarQube instance
		sonar.projectKey=Project_Sonar

		# --- optional properties ---

		# defaults to project key
		sonar.projectName=My project
		
		# defaults to 'not provided'
		sonar.projectVersion=1.0

		# Path is relative to the sonar-project.properties file. Defaults to .
		sonar.sources=src

		# Files to exclude
		sonar.exclusions=src/index.js, src/*.test.js

		# Path of coverage report from a testing library (jest)
		sonar.javascript.lcov.reportPaths = coverage/lcov.info

		# Encoding of the source code. Default is default system encoding
		sonar.sourceEncoding=UTF-8
		```
- NB : Make sure you ran your test cases and have _lcov.info_  coverage report for proper coverage
    > SonarQube doesn't run your tests or generate reports. It only imports pre-generated reports.


##### 3) Run scan using SonarQube
- Navigate to project folder having _sonar-project.properties_ file
- Run command ``` sonar-scanner -Dsonar.login=<token> ```
- It will generate a report and can be viewed from http://localhost:9000



#### Notes : 
- For jest to exclude files, use ```coveragePathIgnorePatterns``` inside package.json of your cra while running test
``` 
    "jest": {
        "coveragePathIgnorePatterns": [
          "node_modules",
          "src/index.js",
          "src/reportWebVitals.js"
        ]
    },

```

- Add a new script ```"coverage": "npm test . -- --coverage",``` and use ```npm run coverage``` for creating coverage report for your app
- Use ```sonar.exclusions``` property to exclude files while running SonarQube

